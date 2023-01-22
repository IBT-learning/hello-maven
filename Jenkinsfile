pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
                git branch: 'feature-genene', changelog: false, credentialsId: 'Github-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
            }
        }
        stage('Verify') {
            steps {
                sh 'ls -lrt'
            }
        }

        stage('Build') {
                    steps {
                        sh 'ls -lrt'
                    }
                }

        stage('Run Test') {
                    steps {
                        sh 'ls -lrt'
                    }
         }
         
         stage('Run mvn commands') {
            steps {
                withMaven(maven: 'maven_3.8.7', mavenSettingsConfig: 'for-maven') {
                // some block
                    sh 'mvn clean'
               }
            }
        }
    }
} 
