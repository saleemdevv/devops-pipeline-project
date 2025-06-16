pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                // This command clones your repository
                git url: 'https://github.com/saleemdevv/devops-pipeline-project.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building the Docker image...'
                // Builds a new image and tags it with the build number
                sh 'docker build -t my-web-app:$BUILD_NUMBER .'
            }
        }
        stage('Deploy New Container') {
            steps {
                echo 'Deploying the new container...'
                script {
                    // This now stops and removes the container ONLY if it exists, and won't fail if it doesn't.
                    sh 'docker stop production-app || true'
                    sh 'docker rm production-app || true'
                    
                    // This runs the new container with the name 'production-app'
                    sh 'docker run -d --name production-app -p 8080:80 my-web-app:$BUILD_NUMBER'
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished. Cleaning up old images...'
            // This cleans up old, unused Docker images to save space
            sh 'docker image prune -af'
        }
    }
}
