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
               bat 'dir'
            }
        }
        stage('Run mvn commands') {
            steps {
                withMaven(maven: 'Maven_3.8.6', mavenSettingsConfig: 'for-Maven') {
                    bat 'mvn clean package install deploy'
                }
            }
        }
        }
    }