pipeline {
  agent any
  stages {
    stage('Code build') {
      steps {
        sh '''cd /opt/aspdotnet
sudo git stash
sudo git pull origin main'''
      }
    }

  }
}