pipeline {
    agent any
    parameters {
    string(name: 'Branch_Name', defaultValue: 'main', description: 'Enter to branch you want to build...')
    choice(name: 'CHOICES', choices: ['one', 'two', 'three'], description: 'choose a number...')
    }
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

               checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/$Branch_Name']], extensions: [], userRemoteConfigs: [[credentialsId: 'ibt-medinat-student', url: 'https://github.com/IBT-learning/hello-maven']])
               sh 'ls -ltr'
               sh 'echo $Branch_Name $CHOICES'
            }

         }
    }
}