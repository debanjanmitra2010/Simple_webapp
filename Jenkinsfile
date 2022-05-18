pipeline {
  agent any 
    tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sshagent(['AWS-Server-Debanjan']) {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
      
      stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/debanjanmitra2010/Simple_webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }

    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
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
