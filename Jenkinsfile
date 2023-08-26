pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/arsalanses/jenkins-pipeline.git']]])
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def imageName = "registry.arsalanses.ir/hashicorp/http-echo"
                    def imageTag = "latest"
                    def dockerImage

                    dockerImage = docker.build("${imageName}:${imageTag}", "-f Dockerfile .")

                    docker.withRegistry('https://registry.arsalanses.ir', 'your-registry-credentials-id') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
