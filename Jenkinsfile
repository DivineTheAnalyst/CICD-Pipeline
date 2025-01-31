pipeline {
    agent {
    label 'worker1'
  }

    environment {
        SONARQUBE_SERVER_URL = 'http://54.221.50.184:9000/'       // Replace with your SonarQube server URL
        SONARQUBE_TOKEN = credentials('SonarQube-Server')         // SonarQube authentication token from Jenkins credentials
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credential') // Docker Hub credentials
        GIT_CREDENTIALS = credentials('github-credentials')                  // GitHub credentials
    }

    stages {
        stage('Checkout Code') {
            steps {
                git credentialsId: 'github-credentials', url: 'https://github.com/DivineTheAnalyst/CICD-Pipeline.git', branch: 'main'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withEnv(['SONAR_LOGIN=${SONARQUBE_TOKEN}']) {
                        sh """
                        echo Running SonarQube Analysis with CLI...
                        /opt/sonar-scanner/bin/sonar-scanner \
                          -Dsonar.projectKey=Project1 \
                          -Dsonar.sources=api,web \
                          -Dsonar.host.url=${SONARQUBE_SERVER_URL} \
                          -Dsonar.login=$SONAR_LOGIN \
                          -Dsonar.inclusions=**/*.py,**/*.html
                        """
                    }
                }
            }
        }

        stage('Build Docker Images with Docker Compose') {
            steps {
                script {
                    sh '''
                    echo "Logging in to DockerHub..."
                    echo "$DOCKERHUB_CREDENTIALS_PSW" | docker login -u "$DOCKERHUB_CREDENTIALS_USR" --password-stdin
                    
                    echo "Building Docker images using docker-compose..."
                    docker compose build
                    '''
                }
            }
        }

        stage('Push Docker Images with Docker Compose') {
            steps {
                script {
                    sh '''
                    echo "Pushing Docker images to DockerHub..."
                    docker compose push
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh '''
                    echo "Setting up kubeconfig..."

                    echo "Applying backend deployment and service..."
                    kubectl apply -f backend-deployment.yaml
                    kubectl apply -f backend-service.yaml

                    echo "Applying frontend deployment and service..."
                    kubectl apply -f frontend-deployment.yaml
                    kubectl apply -f frontend-service.yaml

                    echo "Application deployed successfully!"
                    '''
                }
            }
        }
        stage('Email Notification'){
           steps{
               emailext body: 'The Jenkins pipeline has successfully completed execution on worker1..', subject: 'Jenkins Pipeline Success: CICD-Pipeline', to: 'dnkwocha14@gmail.com'
        }
        }
    post {
        always {
            echo 'Pipeline completed.'
            cleanWs()
        }

    }
}  
}
