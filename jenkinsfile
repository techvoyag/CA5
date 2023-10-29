pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = credentials('DockerHubUsername')
        DOCKERHUB_TOKEN = credentials('DockerHubToken')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Publish Docker Image') {
            steps {
                script {
                    def imageTag = 'latest' 

                    // Build the Docker image with a specific tag
                    docker.build("ca5db:${imageTag}", ".")

                    // Log in to Docker Hub using the provided credentials
                    withCredentials([usernamePassword(credentialsId: 'DockerHubCredentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_TOKEN')]) {
                        // Push the image to Docker Hub
                        docker.withRegistry("https://index.docker.io/v1/", 'DockerHubCredentials') {
                            docker.image("ca5db:${imageTag}").push()
                        }
                    }
                }
            }
        }
    }
}
