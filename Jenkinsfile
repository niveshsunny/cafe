pipeline {
    agent any
    environment {
        appRegistry = "158897922573.dkr.ecr.us-east-1.amazonaws.com/cafe"
        imageName = "mycafe"
        imageTag = "latest"
        dockerHubUsername = "niveshsunny"
        cluster = "cafe"
        service = "cafe"
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
                    sh "docker build -t $dockerHubUsername/$imageName:$imageTag ."
                    sh "docker push $dockerHubUsername/$imageName:$imageTag"
                }
            }
        }
       stage('Deploy to ecs') {
          steps {
              withAWS(credentials: 'awscreds', region: 'us-east-2') {
              sh 'aws ecs update-service --cluster ${cluster} --service ${service} --force-new-deployment'
                 }
             }
       }
    }
}
