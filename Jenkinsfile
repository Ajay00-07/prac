pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ajaykumar2602/myapp1'
        DOCKER_TAG = 'v1'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ajay00-07/prac.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:v1 .'
            }
        }

stage('Login to Docker Hub') {
    steps {
            withCredentials([usernamePassword(credentialsId: 'Dockerhub_PAT', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASSWORD')]) {
            
            // Execute using Windows batch. Notice there is no space before the pipe symbol (|)
            bat 'echo %DOCKER_PASSWORD%| docker login -u %DOCKER_USER% --password-stdin'
        }
}



        stage('Push Docker Image') {
    steps {
        bat 'docker push ajaykumar2602/myapp1:v1'
    }
}
    }

    post {
        success {
            echo 'Docker image v1 built and pushed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
