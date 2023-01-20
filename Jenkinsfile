pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
                echo "cloning"
            }
        }
        stage('Verify') {
            steps {
                sh 'mvn validate'
            }
        }
        stage('Build') {
                    steps {
                        sh 'mvn compile'
                    }
                }

          stage('Sonarqube scan') {
                              steps {
                                  sh 'echo performing sonar scans'
                                  withSonarQubeEnv(credentialsId: 'SQ-student', installationName: 'IBT sonarqube') {
                                      sh "${scannerHome}/bin/sonar-scanner"
                                  }
                              }
                       }

        stage('Run Test') {
                    steps {
                        sh 'mvn test'
                    }
         }
        }
    }
