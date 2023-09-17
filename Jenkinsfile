pipeline {
     agent any
     stages {
       stage('Echo') {
        steps {
            sh 'echo ${MYSQL_URL}'
        }
       }
       stage('Cloning Git') {
         steps {
           git(
            url: 'https://github.com/OleksandraMakovoz/spring-petclinic.git',
            branch: 'main'

           )
         }
       }
        stage('build') {
            steps {
                sh "./mvnw clean compile validate"
            }
        }
        stage('package') {
            steps {
                sh "./mvnw package"
                archiveArtifacts artifacts: '**/target/*.jar'
            }
        }
        stage('deploy') {
            steps {
                 sh "java -jar -Dspring.profiles.active=mysql target/*.jar"
            }
        }
    }
}
