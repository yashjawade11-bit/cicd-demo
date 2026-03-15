pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-demo"
        CONTAINER_NAME = "cicd-demo-app"
    }

    stages {

        stage('Clone') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                bat 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat "docker build -t %IMAGE_NAME%:latest ."
            }
        }

        stage('Stop Old Container') {
            steps {
                echo 'Stopping old container if running...'
                bat "docker stop %CONTAINER_NAME%"
                bat "docker rm %CONTAINER_NAME%"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying new container...'
                bat "docker run -d --name %CONTAINER_NAME% -p 3000:3000 %IMAGE_NAME%:latest"
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}