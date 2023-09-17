pipeline {
     agent any
     stages {
       stage('Echo ENV') {
        steps {
            withAWSParameterStore(credentialsId: 'f41c8ac0-f1ee-4a07-8bbb-1b014d174bfb') {
                          echo sh(script: 'env|sort', returnStdout: true)
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
//         stage('build') {
//             steps {
//                 sh "./mvnw clean compile validate"
//             }
//         }
//         stage('package') {
//             steps {
//                 sh "./mvnw package -DskipTests"
//                 archiveArtifacts artifacts: '**/target/*.jar'
//             }
//         }
//         stage('deploy') {
//             steps {
//                  sh "java -jar -Dspring.profiles.active=mysql target/*.jar"
//             }
//         }
    }
}
