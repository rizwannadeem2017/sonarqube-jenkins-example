pipeline {
    agent any

    stages {
         stage('clone code from git') {
             steps {
                 git url: 'https://github.com/rizwannadeem2017/sonarqube-jenkins-example.git'
        }
    }

         stage('SonarQube analysis') {
              steps {
                  withSonarQubeEnv('mysonar-qube') {
                      sh "./gradlew sonarqube"
            }
        }
    }
    
         stage('Sonar Quality gate') {
              steps {
                  waitForQualityGate abortPipeline: true
              }
         }  
    }

}
