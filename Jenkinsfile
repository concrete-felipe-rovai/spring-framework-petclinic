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

        stage ('Release') {
            steps {
                maven {
                    goals('deploy:deploy-file')
                    property('groupId', 'com.spring.maventest')
                    property('artifactId', 'petclinic')
                    property('version', '1.0.0')
                    property('generatePom', 'false')
                    property('packaging', 'war')
                    property('repositoryId', 'nexus')
                    property('url', 'http://localhost:8081/repository/petclinic/')
                    property('file', 'target/petclinic.war')
                    mavenInstallation("MAVEN")
                    providedSettings('MySettings')
            
                 } 
            }
               
        }
    }
}
