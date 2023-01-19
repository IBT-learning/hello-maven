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
                sh 'ls -lrt'
            }
        }
        stage('Build') {
                    steps {
                        sh 'mvn compile'
                    }
                }

        stage('Sonarqube test') {
                            environment {
                               scannerHome = tool 'ibt-sonarqube';
                            }
                            steps {
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
                sh 'mvn package'
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
