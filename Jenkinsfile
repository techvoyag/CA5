pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from your Git repository
                checkout scm
            }
        }

        stage('Build and Run Docker Compose') {
            steps {
                // Run docker-compose up
                sh 'docker-compose up -d'
            }
        }
    }
}
