pipeline {
    agent any

    stages {
        stage('Git-Clone') {
            steps {
                echo 'cloning'
            }
        }
    stage('Verify') {
            steps {
                sh 'mvn clean validate'
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
                                    sh "${scannerHome}/bin/sonar-scanner"
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
            withMaven(maven: 'Maven_3.9.0', mavenSettingsConfig: 'For-Maven') {
                sh 'mvn clean package install deploy'
            }
            }
        }
        }
    }

