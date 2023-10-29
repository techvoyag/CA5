pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = credentials('DockerHubCredentials')
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
                    def customImageName = "ca5frontend:latest"

                    // Build the Docker image
                    docker.build(customImageName, ".")

                    // Log in to Docker Hub using the provided credentials
                    withCredentials([usernamePassword(credentialsId: 'DockerHubCredentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_TOKEN')]) {
                        // Push the image to Docker Hub
                        docker.withRegistry('https://index.docker.io/v1/', 'DockerHubCredentials') {
                            docker.image(customImageName).push()
                        }
                    }
                }
            }
        }
    }
}
