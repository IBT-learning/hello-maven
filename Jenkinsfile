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
            sh 'echoperforminng sonar scans'
         }
         }
        
        stage('Run test') {
            steps {
            echo "this is a test only"
            }
        }
        }
    }
