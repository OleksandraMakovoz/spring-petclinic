pipeline {
  options {
    buildDiscarder(logRotator(numToKeepStr: '3', artifactNumToKeepStr: '3'))
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
         git(
            url: 'https://github.com/OleksandraMakovoz/spring-petclinic.git',
            branch: 'main'
         )
      }
    }
    stage('Tests') {
      steps {
         sh './mvnw test -Dspring.profiles.active=mysql -DskipTests'
      }
    }
    stage('Build Application') {
      steps {
      withAWSParameterStore(
                  credentialsId: 'f41c8ac0-f1ee-4a07-8bbb-1b014d174bfb',
                  path: '/mysql/',
                  recursive: true,
                  regionName: 'eu-north-1') {
        echo '=== Building Petclinic Application ==='
        sh './mvnw -B -DskipTests clean package'
        archiveArtifacts artifacts: '**/target/*.jar'
        }
      }
    }
    stage('Deploy') {
        steps {
            sh "java -jar -Dspring.profiles.active=mysql target/*.jar"
        }
    }
  }
}
