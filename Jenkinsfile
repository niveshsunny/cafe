pipeline {
    agent any
    environment {
        dockerHubUsername = 'niveshsunny'  // Your Docker Hub username
        imageName = 'mycafe'
        imageTag = 'latest'
    }

    stages {
        stage('Fetch code') {
            steps {
                git branch: 'main', url: 'https://github.com/niveshsunny/cafe.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh "docker build -t $imageName:$imageTag ."
                }
            }
        }

        stage('Upload App Image to Docker Hub') {
            steps {
                script {
                    sh "docker login -u $dockerHubUsername -p 'Nivesh@143'"  // Replace with your Docker Hub password
                    sh "docker build -t niveshsunny/cafe:latest .
                    sh "docker push niveshsunny/cafe:latest"
                }
            }
        }
    }
}
