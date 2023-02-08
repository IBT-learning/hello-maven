pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
             echo "cloning or clowning"
             }
        }

        stage('Verify') {
            steps {
               sh 'validate'
            }
        }

stage('Build') {
            steps {
               sh 'mvn compile'
            }
        }

        stage('Sonarqube scan') {
                    steps {
                       sh 'performing sonar scans'
                    }
                }

        stage('Run mvn commands') {
            steps {
                echo "running maven commands.."
            }
            }
        }
    }