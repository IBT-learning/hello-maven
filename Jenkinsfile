pipeline {
    agent any

       stages {
        stage('Git clone') {
            steps {
                  echo 'cloning'
            }
        }
         stage('Run Test') {

             steps {
                       sh 'ls -lrt'
                    }
                }
                 stage('Run mvn commands') {
                            steps {

                              echo 'running maven commands'
                            }
                 }

        }
    }