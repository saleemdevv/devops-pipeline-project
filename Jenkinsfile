pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                git url: 'https://github.com/saleemdevv/devops-pipeline-project.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building the Docker image...'
                sh 'docker build -t my-web-app:$BUILD_NUMBER .'
            }
        }
        stage('Deploy New Container') {
            steps {
                echo 'Deploying the new container...'
                script {
                    sh 'docker stop production-app || true'
                    sh 'docker rm production-app || true'
                    
                    // THE ONLY CHANGE IS HERE: -p 8081:80
                    sh 'docker run -d --name production-app -p 8081:80 my-web-app:$BUILD_NUMBER'
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished. Cleaning up old images...'
            sh 'docker image prune -af'
        }
    }
}
