pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out your source code from your Git repository
                checkout scm
            }
        }

        stage('Build and Run Docker Containers') {
            steps {
                script {
                    // Run MongoDB Database Service
                    sh 'docker run  techvoyag/ca5db'

                    // Wait for the MongoDB service to start (adjust the sleep time as needed)
                    sleep(time: 30, unit: 'SECONDS')

                    // Run Node.js Application Service
                    sh 'docker run  techvoyag/ca5frontend'
                }
            }
        }
    }

}
