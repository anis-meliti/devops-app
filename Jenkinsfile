node {
    def nodeHome = tool name:'node-14.15.1' , type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
    env.PATH = "${nodeHome}/bin:${env.PATH}"

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
    stage (' run app') {
        sh 'npm start'
    }
}
