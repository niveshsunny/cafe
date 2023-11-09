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
                    // Authenticate with AWS ECR using AWS credentials
                    withCredentials([usernamePassword(credentialsId: 'awscreds', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                        sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $appRegistry"
                    }

                    // Tag the Docker image for ECR
                    sh "docker tag $imageName:$imageTag $appRegistry:$imageTag"

                    // Push the Docker image to ECR
                    sh "docker push $appRegistry:$imageTag"
                }
            }
        }
    }
}
