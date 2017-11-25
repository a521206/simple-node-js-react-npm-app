pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }
    
  }
  
  
      parameters {
        booleanParam(defaultValue: true, description: '', name: 'userFlag')
    }

  stages {
   stage("foo") {
            steps {
                echo "flag: ${params.userFlag}"
            }
        }
    
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
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
  }
  environment {
    CI = 'true'
  }
}
