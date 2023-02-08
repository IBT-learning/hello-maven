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
                       sh 'echo performing sonar scans'
                    }
                }

        stage('Run mvn commands') {
            steps {
                echo "running maven commands.."
            }
            }
        }
    }