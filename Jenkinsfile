pipeline {
    agent any

       stages {
        stage('Git clone') {
            steps {
                  echo 'cloning'
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
                       sh 'echo performing sonar scan'
                       withSonarQubeEnv(credentialsId: 'SQ-student', installationName: 'IBT sonarqube') {
                          sh "${scannerHome}/bin/sonar-scannerHome"
                       }
                    }
                }
         stage('Run Test') {

             steps {
                       sh 'mvn test'
                    }
                }
                 stage('Run mvn commands') {
                            steps {

                              echo 'running maven commands'
                            }
                 }

        }
    }