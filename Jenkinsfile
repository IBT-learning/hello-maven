pipeline {
    agent any
    stages {
        stage('Validate') {
            steps {
                sh 'mvn validate'
            }
        }
        stage('Compile') {
             steps {
                 sh 'mvn compile'
             }
        }
    }
}