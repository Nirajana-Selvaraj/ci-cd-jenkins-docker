pipeline {
    agent any

    environment {
        IMAGE_NAME = "yourdockerhubusername/ci-cd-app"
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/yourusername/ci-cd-jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running basic tests (Placeholder)'
                sh 'echo Tests Passed!'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    script {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 yourdockerhubusername/ci-cd-app:latest'
            }
        }
    }
}