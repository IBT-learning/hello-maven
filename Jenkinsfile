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
               ls -lrt
            }
        }

        stage('Build') {
                    steps {
                       bat 'dir'
                    }
                }

        stage('Run mvn commands') {
            steps {
                echo "running maven commands.."
            }
            }
        }
    }