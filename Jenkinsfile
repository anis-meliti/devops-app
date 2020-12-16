pipeline {
    def nodeHome = tool name:'node-14.15.1' , type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
    env.PATH = "${nodeHome}/bin:${env.PATH}"
    def d = new Date().format( 'yyyyMMdd' )

    stage ('checkout tools') {
        sh 'node -v'
        sh 'npm -v'
    }

    stage ('checkout') {
        checkout scm
    }
    stage ('npm install') {
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
