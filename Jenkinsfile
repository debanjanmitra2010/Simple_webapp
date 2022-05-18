pipeline {
  agent any 
  stages {
    stage ('Initialize') {
      steps {
        sshagent(['AWS-Server-Debanjan']) {
        sh '''
                    ubuntu@54.165.222.36:echo "PATH = ${PATH}"
                    ubuntu@54.165.222.36:echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    }
    
    stage ('Build') {
      steps {
        sshagent(['AWS-Server-Debanjan']) {
      sh 'ubuntu@54.165.222.36:mvn clean package'
       }
      }
    }
    
        stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@54.144.242.76:/prod/webapps/webapp.war'
              }      
           }       
    }

  }
}
