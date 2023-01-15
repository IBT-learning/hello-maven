pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
                git branch: 'gunj-app', changelog: false, credentialsId: 'GitHub-creds', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
            }
        }
        stage('List files') {
            steps {
                sh 'ls -lrt'
            }
        }
         stage('Run mvn commands') {
            steps {
                sh 'source ~/.bash_profile && mvn clean'
                
            }
            }
        }
    }
