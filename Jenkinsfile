pipeline {
    agent any

    stages {
        stage('Git-Clone') {
            steps {
                git branch: 'feature-nnamdi', changelog: false, credentialsId: 'GitHub-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
                echo 'Hello World'
            }
        }
        stage('List files') {
            steps {
                bat 'dir'
                echo 'Hi, this is Nnamdi'
            }
        }
        
    }
}
