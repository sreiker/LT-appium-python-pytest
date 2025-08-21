pipeline {
  agent any

  stages {
    stage('buildNumber') {
            steps {
                script {
                    // Store the Jenkins build number in a variable
                    def myBuildNumber = "BUILD_NAME"

                    // Now you can use 'myBuildNumber' for further processing
                    echo "Current build number is: ${myBuildNumber}"
                }
            }
        }
    stage('Checkout') {
      steps {
        checkout([$class: 'GitSCM',
                  branches: [[name: '*/main']],
                  userRemoteConfigs: [[url: 'https://github.com/sreiker/python']]])
      }
    }

    stage('Test') {
      steps {
        sh 'python3 -m pip install selenium'
        sh 'python3 -m pip install pytest'
        sh 'python3 test1.py'
      }
    }
    stage('Report'){
    steps{
      lambdaTestReportPublisher 'automation'
    }
    }
  }
  }
