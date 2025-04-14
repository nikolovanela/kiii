pipeline {
    agent any

    environment {
        registry = "nikolovanela/kiii"
        registryCredential = 'dockerhub'
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Build image') {
            steps {
                script {
                    app = docker.build("${registry}:latest")
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }

        stage('Clean up') {
            steps {
                cleanWs() // Чистење на работната папка
            }
        }
    }
}
