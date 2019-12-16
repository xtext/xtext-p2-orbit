pipeline {
  agent {
    kubernetes {
      label 'migration'
    }
  }
  
  options {
    buildDiscarder(logRotator(numToKeepStr:'5'))
    disableConcurrentBuilds()
    timeout(time: 30, unit: 'MINUTES')
    timestamps()
  }

  stages {
    stage('Perform') {
      steps {
        checkout scm
        
        dir ('updates') {
          sshagent(['projects-storage.eclipse.org-bot-ssh']) {
            sh 'scp -r . genie.xtext@projects-storage.eclipse.org:/home/data/httpd/download.eclipse.org/modeling/tmf/xtext/updates/'
          }
        }
      } // steps
    } // stage
  } // stages
}

