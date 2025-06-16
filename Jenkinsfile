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
                    // This checks if an old container named 'production-app' exists and stops/removes it
                    def oldContainer = sh(script: 'docker ps -q --filter name=production-app', returnStatus: true)
                    if (oldContainer == 0) {
                        sh 'docker stop production-app && docker rm production-app'
                    }
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
