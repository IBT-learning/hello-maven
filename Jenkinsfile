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
                        sh 'mvn compile'
                    }
                }

        stage('Run Test') {
                    steps {
                        sh 'mvn test'
                    }
         }
        }
    }
