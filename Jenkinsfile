pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
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
