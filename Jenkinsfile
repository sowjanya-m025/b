pipeline {
    agent any

    environment {
        IMAGE = "sowjanya2510/my-nginx-app"
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
                sh 'docker build -t my-nginx-app .'
            }
        }

        stage('Tag') {
            steps {
                // Tag the image for Docker Hub
                 sh "docker tag my-nginx-app ${IMAGE}"
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
