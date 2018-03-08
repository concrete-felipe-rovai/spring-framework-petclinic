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
                sh 'mvn deploy:deploy-file -DgroupId=com.somecompany -DartifactId=petclinic -Dversion=1.0.0 -DgeneratePom=False -Dpackaging=war -DrepositoryId=nexus -Durl=http://localhost:8081/repository/maven-releases/ -Dfile=target/petclinic.war'
            }
               
        }
    }
}
