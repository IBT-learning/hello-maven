pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Hi') {
            steps {
                echo 'Hello there'
            }
        }
         stage('test') {
              steps {
                        echo 'testing the added jenkins file'
              }
         }
         stage('checkout github'){
             steps {

               checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/feature-medinat']], extensions: [], userRemoteConfigs: [[credentialsId: 'ibt-medinat-student', url: 'https://github.com/IBT-learning/hello-maven']])
               sh 'ls -ltr'
            }

         }
    }
}