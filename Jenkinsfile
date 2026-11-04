
pipeline {
    triggers {
    pollSCM('H/1 * * * *')
}
    agent any

    environment {
        IMAGE_NAME = 'experiment13-web'
        CONTAINER_NAME = 'experiment13-container'
    }

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                deleteDir()

                git branch: 'main',
                    url: 'https://github.com/AbzamA/Experiment13-CICD.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t experiment13-web .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing website'
                sh 'test -f index.html'
                echo 'Website test passed'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website'
                sh 'docker rm -f experiment13-container || true'
                sh 'docker run -d --name experiment13-container -p 8082:80 experiment13-web'
            }
        }
    }

    post {
        success {
            echo 'Experiment 13 CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the failed stage.'
        }
    }
}
