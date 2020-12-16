pipeline {
    environment {
        registry = 'https://hub.docker.com/r/ansmeliti/first-demo-app'
        registryCredential = ''
        dockerImage = ''
    }
    def d = new Date().format( 'yyyyMMdd' )
    agent any
    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/anis-meliti/devops-app.git'
            }
        }
        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$d"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps {
                sh "docker rmi $registry:$d"
            }
        }
    }
}
