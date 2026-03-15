pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                echo 'Cloning repository'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies'
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                bat 'docker build -t cicd-demo .'
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running container'
                bat 'docker run -d -p 3000:3000 cicd-demo'
            }
        }

    }
}
