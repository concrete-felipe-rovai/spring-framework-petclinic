pipeline {
    agent any
    tools {
        maven 'MAVEN'
        jdk 'jdk8'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn install' 
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
        
        stage ("Nexus Publish"){
            steps{
                  sh "echo $BUILD_NUMBER"
                  sh "curl -u jenkins:jenkins -X PUT "http://localhost:8081/artifactory/libs-release/petclinic/ROOT.war" -T petclinic.war"
                }   
            }
        }  
}

