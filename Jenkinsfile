pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

    stage('Staging Central Region') {
      parallel {
        stage('Regular Staging') {
          steps {
            sh 'ls'
          }
        }

        stage('GovCloud Staging') {
          steps {
            sh 'ls'
          }
        }

      }
    }

    stage('Approval') {
      steps {
        input(message: 'Please approve', ok: 'OK')
      }
    }

    stage('Canary Central Region') {
      parallel {
        stage('Canary Central Region') {
          steps {
            sh 'ls'
          }
        }

        stage('Canary GovCloud') {
          steps {
            sh 'ls'
          }
        }

      }
    }

    stage('Validation') {
      steps {
        sh 'ls'
        sh 'ls'
      }
    }

    stage('Load Central Region') {
      parallel {
        stage('Load Central Region') {
          steps {
            sh 'ls'
          }
        }

        stage('Load GovCloud') {
          steps {
            sh 'ls'
          }
        }

      }
    }

    stage('Load complete') {
      steps {
        sh 'ls'
      }
    }

  }
}