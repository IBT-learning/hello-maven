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
                        bat 'mvn compile'
             
            }
          }
	 stage('sonarqube scan by bokovi') {
		 environment {
                        scannerHome = tool 'ibt-sonarqube';
            steps {
                bat 'echo running maven commands'
                 withSonarQubeEnv(credentialsId: 'SQ-student') {
			 bat "${scannerHome}/bin/sonar-scanner"
}

        }
    }
stage('Run Test') {
                    steps {
                        bat 'mvn test'
