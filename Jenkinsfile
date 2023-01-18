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
                        sh 'ls -lrt'
                    }
                }

        stage('Run Test') {
                    steps {
                        sh 'ls -lrt'
                    }
         }
         stage('Run mvn commands') {
            steps {
                echo "running maven commands"
            }
            }
        }
    }
