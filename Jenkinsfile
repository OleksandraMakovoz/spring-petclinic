pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "./mnnw clean compile validate"
            }
        }
        stage('test') {
            steps {
                sh "./mnnw test"
            }
        }
        stage('package') {
            steps {
                sh "./mnnw package"
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
