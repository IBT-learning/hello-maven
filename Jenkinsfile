pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
                git branch: 'feature-fancy', changelog: false, credentialsId: 'GitHub-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
            }
        }
        stage('List directories') {
            steps {
               bat 'dir '
            }
        }
            }
        }