node {
    def app
    stage('Clone repository') {
        checkout scm
    }
     stage('Build image') {
         if (env.BRANCH_NAME == 'dev') {
         steps {
             app = docker.build("bxbi/kiii-labs")
         }
         }
         else{
             echo 'This is not a dev branch'
         }
    }
    stage('Push image') {  
        if (env.BRANCH_NAME == 'dev') {
        steps{
            docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                  // signal the orchestrator that there is a new version
               }
        }
         }
         else{
             echo 'This is not a dev branch'
         }
      }
 } 

