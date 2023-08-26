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

                    def registryURL = 'https://registry.arsalanses.ir'
                    def registryCredentials = [
                        usernamePassword(
                            credentialsId: '',
                            usernameVariable: 'REGISTRY_USERNAME',
                            passwordVariable: 'REGISTRY_PASSWORD'
                        )
                    ]
                    
                    docker.withRegistry(registryURL, registryCredentials) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
