node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    if (env.BRANCH_NAME == 'dev') {
        stage('Build image') {
            steps {
                app = docker.build("bxbi/kiii-labs")
            }
        }
        stage('Push image') {
            steps{
                docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                    app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    app.push("${env.BRANCH_NAME}-latest")
                    // signal the orchestrator that there is a new version
                }
            }
        }
    }
    else{
        echo 'This is not a dev branch'
    }
} 

