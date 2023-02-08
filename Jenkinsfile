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
               bat 'dir'
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