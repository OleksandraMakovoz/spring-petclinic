pipeline {
  options {
    buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
  }
  agent any
  stages {
    stage('Echo') {
      steps {
        script {
          withAWSParameterStore(
            credentialsId: 'f41c8ac0-f1ee-4a07-8bbb-1b014d174bfb',
            path: '/mysql/',
            recursive: true,
            regionName: 'eu-north-1') {
              echo sh(script: 'env|sort', returnStdout: true)
            }
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
    stage('Tests') {
      steps {
         sh './mvnw test'
      }
    }
    stage('Build Application') {
      steps {
        echo '=== Building Petclinic Application ==='
        sh './mvnw -B -DskipTests clean package'
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
