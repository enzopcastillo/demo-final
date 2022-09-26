pipeline {
    agent any

    stages {
        stage('Clone repository') { 
            steps { 
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_credentials', url: 'https://github.com/enzopcastillo/demo-final']]])
                }
            }
        }
        stage('Build') { 
            steps { 
                script{
                 app = docker.build("enzopcastillo/demo-final")
                }
            }
        }
        stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://registry.hub.docker.com/', 'dockerhub_credentials') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}