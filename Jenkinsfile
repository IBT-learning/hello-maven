pipeline {
    agent any
    stages {
        stage('Validate') {
            steps {
                sh 'mvn validate'
            }
        }
        stage('Compile') {
             steps {
                 sh 'mvn compile'
             }
        }
        stage('Test') {
              steps {
                 sh 'mvn test'
              }
        }
        stage('SonarQube Analysi'){
            environment{
                sonarScan = tool 'sonarqube-scanner-me'
               }
              steps{
                 withSonarQubeEnv(credentialsId: 'sonar-key', installationName:'sonar-server') {
                    sh "${env.sonarScan}/bin/sonar-scanner"
                 }
              }

        }
    }
}