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
                    environment {
                                   scannerHome = tool 'ibt-learning';
                    }
                    steps {
                       sh 'echo performing sonar scan'
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
                 stage('upload to artifactory') {
                            steps {
                              configFileProvider([configFile('5d0920bc-97c5-4877-8aa4-2f61975fa9fc')]) {
                                  sh 'mvn package'
                                  sh 'mvn deploy'
                              }
                            }
                 }
              stage ('OWASP Dependency-Check Vulnerabilities') {
                                  steps {
                                      dependencyCheck additionalArguments: '''
                                          -o "./"
                                          -s "./"
                                          -f "ALL"
                                          --prettyPrint''', odcInstallation: 'dependency-check'

                                      dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                                  }
                              }
        }
    }