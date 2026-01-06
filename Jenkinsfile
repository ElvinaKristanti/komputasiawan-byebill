pipeline {
    agent any

    environment {
        IMAGE_NAME = "ayundha/komputasi-image:latest"
    }

    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Run Tests (Optional)') {
            steps {
                bat 'echo Testing application...'
            }
        }

        stage('Deploy') {
            steps {
                bat 'echo Deploy step here'
            }
        }

        /* ===== TAMBAHAN AGAR AZURE BISA AKSES ===== */

        stage('Login Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%'
            }
        }
    }
}
