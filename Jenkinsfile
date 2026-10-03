pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-web:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop devops-web-container || true'
                sh 'docker rm devops-web-container || true'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d --name devops-web-container -p 80:80 devops-web:latest'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {

        success {
            echo 'Deployment completed successfully.'
        }

        failure {
            echo 'Deployment failed.'
        }
    }
}