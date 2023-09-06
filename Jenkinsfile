pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                ./mnnw clean compile validate
            }
        }
        stage('test') {
            steps {
                ./mnnw test
            }
        }
        stage('package') {
            steps {
                ./mnnw package
            }
        }
        stage('deploy') {
            steps {
                 java -jar -Dspring.profiles.active=mysql target/*.jar
            }
        }
    }
}
