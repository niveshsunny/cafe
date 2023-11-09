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

        stage('Upload App Image to ECR') {
            steps {
                script {
                     sh 'aws ecr get-login-password--region us-east-1 | docker login --username AWS --password-stdin 158897922573.dkr.ecr.us-east-1.amazonaws.com/cafe:latest'
                sh 'docker push 158897922573.dkr.ecr.us-east-1.amazonaws.com/cafe:latest'
                }
            }
        }
    }
}
