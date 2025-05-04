pipeline {
    agent any

    environment {
        IMAGE_NAME = "nirajana23/ci-cd-app"
    }

    stages {
        stage('Clone') {
            steps {
               git 'git credentialsId: 'github-credentials', url: 'https://github.com/Nirajana-Selvaraj/ci-cd-jenkins-docker.git''

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
               sh 'docker run -d -p 5000:5000 Nirajana-Selvaraj/ci-cd-app:latest'

            }
        }
    }
}
