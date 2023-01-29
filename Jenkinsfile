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
                echo "bokovi is verifying"
            }
        }

        stage('Build') {
                    steps {
                        sh 'mvn compile'
             
                   }
             }
	    
	 // Running sonarqube
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
               stage('upload to artifactory') {
                             steps {
                                 //sh 'mvn test'
                                 configFileProvider([configFile('5d0920bc-97c5-4877-8aa4-2f61975fa9fc')]) {
                                     sh 'mvn package'
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
