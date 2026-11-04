
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'experiment13-web'
        CONTAINER_NAME = 'experiment13-container'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading source code from GitHub'
                git branch: 'main',
                    url: 'https://github.c.com/AbzamA/Experiment13-CICD.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker Image'
                sh 'docker build -t experiment13-web .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing website files'
                sh 'test -f index.html'
                sh 'echo Website test passed'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website using Docker'
                sh 'docker rm -f experiment13-container || true'
                sh 'docker run -d --name experiment13-container -p 8082:80 experiment13-web'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed. Check the console output.'
        }
    }
}
