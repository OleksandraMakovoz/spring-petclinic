pipeline {
     agent any
     stages {
       stage('Echo') {
        steps {
            withAWSParameterStore(credentialsId: '362447113011',
                 regionName: 'eu-north-1') {
                          sh 'echo ${MYSQL_URL}'
                 }
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
