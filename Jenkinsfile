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
	 }
 }	
