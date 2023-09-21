pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from the repository
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                    def imageName = 'my-node-app'
                    def dockerImage = docker.build(imageName, '.')
                    dockerImage.push()
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run the Docker container
                script {
                    def imageName = 'my-node-app'
                    def container = docker.image(imageName).run('-p 8080:3000', '--name my-node-app-container')
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker resources
            script {
                def imageName = 'my-node-app'
                docker.image(imageName).remove()
                docker.container('my-node-app-container').stop()
                docker.container('my-node-app-container').remove()
            }
        }
    }
}
