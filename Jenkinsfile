pipeline {
    def d = new Date().format( 'yyyyMMdd' )

    stage ('checkout tools') {
        sh 'node -v'
        sh 'npm -v'
    }

    stage ('checkout') {
        checkout scm
    }
    stage ('install') {
        sh 'npm install'
    }
    stage ('run build') {
        sh 'npm run build'
    }
    stage ('docker build/push') {
        docker.withRegistry('https://index.docker.io', 'dockerhub') {
            docker.build("ansmeliti/first-demo-app:${d}", '.').push()
        }
    }
}
