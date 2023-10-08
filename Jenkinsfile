pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout your Git repository
                checkout scm
            }
        }
        stage('Build') {
            steps {
                // Add build steps here (e.g., compile code)
                sh 'echo "Building..."'
            }
        }
        stage('Test') {
            steps {
                // Add test steps here
                sh 'echo "Testing..."'
            }
        }
        stage('Deploy') {
            steps {
                // Add deployment steps here (e.g., deploying to AWS)
                sh 'echo "Deploying..."'
            }
        }
    }
}

