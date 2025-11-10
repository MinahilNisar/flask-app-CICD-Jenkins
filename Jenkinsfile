pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "flask-app-ci-cd:latest"
    }

    stages {                  // <-- stages block starts here
        stage('Checkout') {
            steps {
                git url: 'https://github.com/MinahilNisar/flask-app-CICD-Jenkins.git',
                    branch: 'main',
                    credentialsId: 'cfa67216-f3f2-4d71-a601-2ab7e9100b4a'
            }
        }

        stage('Setup Python') {
            steps {
                bat 'python -m venv venv'
                bat 'venv\\Scripts\\python -m pip install --upgrade pip'
                bat 'venv\\Scripts\\python -m pip install -r requirements.txt'

            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Run Docker Container') {
            steps {
                bat "docker run -d -p 5000:5000 ${DOCKER_IMAGE}"
            }
        }
    } // <-- stages block ends here

    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
} // <-- pipeline block ends here
