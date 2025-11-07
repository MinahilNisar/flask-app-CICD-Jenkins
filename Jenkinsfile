pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning Repository...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                bat 'docker build -t flask-app-cicd .'
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running container...'
                bat 'docker run -d -p 5000:5000 --name flask-container flask-app-cicd'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing container...'
                //bat 'curl http://localhost:5000'
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Cleaning up...'
                bat 'docker stop flask-container && docker rm flask-container'
            }
        }
    }

    post {
        always {
            echo 'CI/CD Pipeline Completed'
        }
    }
}
