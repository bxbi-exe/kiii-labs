node {
    def app
    when{
        expression {
                env.BRANCH_NAME == 'dev' 
              }
    }
    stages {
        stage('Clone repository') {
           checkout scm
        }
        stage('Build image') {
           app = docker.build("bxbi/kiii-labs")
        }
        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    }
    when{
        expression {
                env.BRANCH_NAME != 'dev' 
              }
    }
    stages {
        stage('Not dev') {
           checkout scm
        }
    }
}
