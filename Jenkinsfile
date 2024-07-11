pipeline {
    agent any
    environment {
          version='1.1.0'
        }
      tools {
        maven 'Maven_3.9'
      }
    parameters {
    string(name: 'Branch_Name', defaultValue: 'main', description: 'Enter to branch you want to build...')
    choice(name: 'CHOICES', choices: ['one', 'two', 'three'], description: 'choose a number...')
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                echo "App version is ${version}"
            }
        }
        stage('Hi') {
            steps {
                echo 'Hello there'
            }
        }
         stage('maven') {
             steps {
                 sh 'mvn --version'
                 }
             }
         stage('test') {
         when{
            expression {
                '$Branch_Name'=='main'
            }

         }
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
    post{
      always{
         echo "build successful"
      }

    }
}


