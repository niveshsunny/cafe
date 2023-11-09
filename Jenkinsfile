pipeline {
    agent any
    environment {
        appRegistry = "158897922573.dkr.ecr.us-east-1.amazonaws.com/cafe"
        imageName = "mycafe"
        imageTag = "latest"
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
