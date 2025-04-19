pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'kovidag13/nit-app:latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: 'github-creds', url: 'https://github.com/kovidaG13/GradeGuard-Analytics.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('', 'docker-creds') {
                        sh 'docker push $DOCKER_IMAGE'
                    }
                }
            }
        }
    }
}
