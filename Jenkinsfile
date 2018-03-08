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
                    sh " curl -v  -X PUT -F r=releases -F g=com.petclinic -F a=widget -F v=1.0.0 -F p=jar -F file=petclinic.war -u jenkins:jenkins http://localhost:8081/repository/maven-releases/com/petclinic/petclinic-${BUILD_NUMBER}.war "
                }   
            }
        }  
}
