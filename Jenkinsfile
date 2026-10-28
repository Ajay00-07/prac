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
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub_pat',
            usernameVariable: 'DOCKERHUB_USERNAME',
            passwordVariable: 'DOCKERHUB_TOKEN'
        )]) {
            powershell '''
                $token = $env:DOCKERHUB_TOKEN.Trim()
                $token | docker login -u $env:DOCKERHUB_USERNAME --password-stdin
                if ($LASTEXITCODE -ne 0) {
                    exit $LASTEXITCODE
                }
            '''
        }
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
