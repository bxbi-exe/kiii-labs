node {
    def app
    stage('Clone repository') {
        checkout scm
    }
     stage('Build image') {
         when { branch 'dev' }
         app = docker.build("mjovanovik/kiii-jenkins")
    }
    stage('Push image') {  
        when { branch 'dev' }
         docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
              app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
               app.push("${env.BRANCH_NAME}-latest")
              // signal the orchestrator that there is a new version
           }
      }
 } 

