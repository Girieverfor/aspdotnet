pipeline {
  agent any
  stages {
    stage('Code build process') {
      parallel {
        stage('Code build process') {
          steps {
            sh '''cd /opt/aspdotnet
sudo git stash
sudo git pull origin main'''
          }
        }

        stage('Code commit status') {
          steps {
            sh '''cd /opt/aspdotnet
export GIT_COMMIT=$(git rev-parse --short HEAD)
echo $GIT_COMMIT'''
          }
        }

      }
    }

    stage('Docker build API') {
      parallel {
        stage('Docker build API') {
          steps {
            sh '''cd /opt/aspdotnet
sudo docker build -t 9011603079/testing-repo:customerapi -f src/CustomersAPI/Dockerfile .
'''
          }
        }

        stage('Docker build MVC') {
          steps {
            sh '''cd /opt/aspdotnet
sudo docker build -t 9011603079/testing-repo:customermvc -f src/CustomersMVC/Dockerfile .
'''
          }
        }

      }
    }

    stage('Docker push API/MVC') {
      steps {
        sh '''sudo docker push 9011603079/testing-repo:customerapi
sudo docker push 9011603079/testing-repo:customermvc'''
      }
    }

    stage('Deploy into k8s') {
      steps {
        sh '''sudo kubectl rollout restart deployment/customerapi -n stag
sudo kubectl rollout restart deployment/customermvc -n stag
'''
      }
    }

  }
}