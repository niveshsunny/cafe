pipeline {
    agent any
    environment {
        registryCredential = 'ecr:us-east-1:awscreds'
        appRegistry = "158897922573.dkr.ecr.us-east-1.amazonaws.com/cafe"
        caferegistry = "https://158897922573.dkr.ecr.us-east-1.amazonaws.com"
        cluster = "mynewcluster"
        service = "vprofileappsvc"
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
                    def imageName = 'mycafe'
                    def imageTag = 'latest'
                    sh "docker build -t ${imageName}:${imageTag} ."
                }
            }
        }

        stage('Upload App Image to ECR') {
            steps {
                script {
                    // Define the image name
                    def imageName = 'mycafe'


                    // Tag the Docker image for ECR
                    sh "docker tag ${imageName}:${imageTag} $appRegistry:${imageTag}"

                    // Push the Docker image to ECR
                    sh "docker push $appRegistry:${imageTag}"
                }
            }
        }
    }
}

