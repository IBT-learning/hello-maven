pipeline {
    agent any

       stages {
        stage('Git clone') {
            steps {
                  echo 'cloning'
            }
        }

          stage('DevOps') {
                    steps {
                       echo 'DevOps is more like a cultural shift that enhances collaboration between development and operations in agile organizations'
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
                   environment {
                                  scannerHome = tool 'ibt-sonarqube';
                    }

                    steps {
                       sh 'echo performing sonar scans'
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