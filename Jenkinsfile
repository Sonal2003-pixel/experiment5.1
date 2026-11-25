pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'sonaldsilva/experiment5repo'
        DOCKER_CREDENTIALS = 'dockerhub_credentials'
        DOCKER_CMD = '"C:\\Users\\pauld\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe"'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sonal2003-pixel/experiment5.1.git'
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                bat 'dir'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '%DOCKER_CMD% build -t %DOCKER_IMAGE%:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub_credentials',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat '%DOCKER_CMD% login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat '%DOCKER_CMD% push %DOCKER_IMAGE%:latest'
                    bat '%DOCKER_CMD% logout'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline execution failed!'
        }
    }
}
