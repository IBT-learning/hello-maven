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
               sh 'dir'
            }
        }

        stage('Build maven code') {
                    steps {
                       mvn clean install
                    }
                }
        stage('Run mvn commands') {
            steps {
                echo "running maven commands.."
            }
            }
        }
    }