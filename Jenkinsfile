pipeline {
    environment {
        registry = 'https://hub.docker.com/r/ansmeliti/first-demo-app'
        registryCredential = ''
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/anis-meliti/devops-app.git'
            }
        }
        stage('Building our image') {
            def d = new Date().format( 'yyyyMMdd' )
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
