pipeline {
    agent any

    stages {
        stage ('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("abastosdiego/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage {
            script {
                docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")
                }
            }
        }
    }
}