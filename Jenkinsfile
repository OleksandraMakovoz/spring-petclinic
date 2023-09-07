pipeline {
    agent {
        label 'ubuntu'
    }
    stages {
        stage('build') {
            steps {
                sh "./mvnw clean compile validate"
            }
        }
        stage('test') {
            steps {
                sh "./mvnw test"
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
