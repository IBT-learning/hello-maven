pipeline {
    agent any
    stages {
        stage('Git clone') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Validate') {
                    steps {
                        sh 'mvn validate'
                    }
                }
        stage('Compile code') {
                            steps {
                                sh 'mvn compile'
                            }
                        }
         stage('Run Tests') {
                             steps {
                                 sh 'mvn test'
                             }
                         }
         stage('Create Artifact') {
                             steps {
                                 sh 'mvn package'
                             }
                         }
    }
}