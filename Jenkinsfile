pipeline {
    agent any

    environment {
        IMAGE = "sowjanya2510/myapp:v1"
        CREDS = "dockerhub-creds"
        // Ensure Jenkins can find Docker CLI
        PATH = "/usr/local/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                // Checkout your main branch
                git branch: 'main', url: 'https://github.com/sowjanya-m025/b.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build Docker image
                sh 'docker build -t myapp .'
            }
        }

        stage('Tag') {
            steps {
                // Tag the image for Docker Hub
                 sh "docker tag myapp ${IMAGE}"
            }
        }

        stage('Login') {
            steps {
                // Login to Docker Hub using Jenkins credentials
                withCredentials([usernamePassword(
                    credentialsId: CREDS,
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }
        
        stage('Push') {
            steps {
                // Push the image to Docker Hub
                sh "docker push ${IMAGE}"
            }
        }
    }
} 
