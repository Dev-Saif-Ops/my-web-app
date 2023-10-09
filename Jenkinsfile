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
                // Build Docker image with a version tag
                sh 'docker build -t my-web-app:${BUILD_NUMBER} .'
    
                // Run unit tests
                sh 'npm test'  // Replace with your actual test command
            }
        }
        stage('Push to ECR') {
            steps {
                // Authenticate Docker to your ECR registry (as described earlier)
                sh 'aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin your-account-id.dkr.ecr.your-region.amazonaws.com'
    
                // Tag your Docker image for ECR
                sh 'docker tag my-web-app:${BUILD_NUMBER} your-account-id.dkr.ecr.your-region.amazonaws.com/my-web-app-repo:${BUILD_NUMBER}'
    
                // Push the image to ECR
                sh 'docker push your-account-id.dkr.ecr.your-region.amazonaws.com/my-web-app-repo:${BUILD_NUMBER}'
            }
        }
        stage('Deploy to EC2') {
            steps {
                // SSH into your EC2 instance and deploy the Docker container (as described earlier)
                sh 'ssh -i "your-key.pem" ubuntu@your-ec2-public-ip "docker pull your-account-id.dkr.ecr.your-region.amazonaws.com/my-web-app-repo:${BUILD_NUMBER}"'
                sh 'ssh -i "your-key.pem" ubuntu@your-ec2-public-ip "docker run -d -p 80:3000 your-account-id.dkr.ecr.your-region.amazonaws.com/my-web-app-repo:${BUILD_NUMBER}"'
            }
        }
        stage('Validation') {
            steps {
                // Run automated tests or validation scripts
                sh 'curl http://your-ec2-public-ip:80'  // Replace with your validation command
            }
        }
    }
}

