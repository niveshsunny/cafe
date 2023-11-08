pipeline {
    agent any

    stages {
        stage('Fetch code') {
            steps {
                git branch: 'main', url: 'git@github.com:niveshsunny/cafe.git'
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
    }
}

