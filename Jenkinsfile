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
                        echo "bokovi is building"
                    }
                }

        stage('Run Test') {
                    steps {
                        echo "bokovi is testing"
                    }
         }
         stage('Run mvn commands') {
            steps {
                echo "running maven commands"
            }
         }

	    stage('another test from bokovi') {
            steps {
                echo "running maven commands"
            }
          }
         stage('third test from bokovi') {
            steps {
                echo "running maven commands"
            }
          }
	 stage('sonarqube scan by bokovi') {
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
