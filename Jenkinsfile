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
                  userRemoteConfigs: [[url: 'https://github.com/sreiker/LT-appium-python-pytest']]])
      }
    }

    stage('Test') {
      steps {
        sh 'python3 -m pip install Appium-Python-Client'
        sh 'pip3 install pytest'
        sh 'pytest tests/test_android.py'
      }
    }
    stage('Report'){
    steps{
      lambdaTestReportPublisher 'automation'
    }
    }
  }
  }
