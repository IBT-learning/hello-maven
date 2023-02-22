pipeline {
    agent any
    stages {
        stage('Git clone') {
            steps {
                echo 'Hello World'
            }
        }
        stage('mvn validate') {
                    steps {
                        sh 'mvn validate'
                    }
                }
    }
}