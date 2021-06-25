pipeline {
    agent any
    environment {
        
        DOCKER_IMAGE_NAME = "rizwan1989/riz-tomcat"
        registry = "registry.hub.docker.com/rizwan1989/riz-tomcat"
        
       
    }

    stages {
         stage('clone code from git') {
             steps {
                 git url: 'https://github.com/rizwannadeem2017/sonarqube-jenkins-example.git'
        }
    }

         stage('SonarQube analysis') {
              steps {
                  withSonarQubeEnv('sonarQube') {
                      sh "./gradlew sonarqube"
            }
        }
    }
    
         stage('Sonar Quality gate') {
              steps {
                  waitForQualityGate abortPipeline: true
              }
         }

         stage('Build Docker Image') {
           
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    
                }
            }
        }
         stage('Push Docker Image') {
            
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                          app.push("${env.BUILD_NUMBER}")
                        //app.push("apiv1")
                    }  
                }
            } 
         }       
    }
}
