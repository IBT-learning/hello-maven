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
	 stage('sonarqube scan by bokovi') {
		 environment {
                        scannerHome = tool 'ibt-sonarqube';
            steps {
               echo "running maven commands"
                 withSonarQubeEnv(credentialsId: 'SQ-student') {
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
