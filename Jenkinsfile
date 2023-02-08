pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
                git branch: '${Branch}', changelog: false, credentialsId: 'GitHub-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
            }
        }
        stage('Verify') {
            steps {
               bat 'dir'
            }
        }

        stage('Build') {
                    steps {
                       bat 'dir'
                    }
                }

        stage('Run Test') {
        when {
             expression {
                   BRANCH_NAME == 'master'
              }
             }
                    steps {
                       bat 'dir'
                    }
                }
        stage('Run mvn commands') {
            steps {
                withMaven(maven: 'Maven_3.8.6', mavenSettingsConfig: 'for-Maven') {
                    bat 'mvn clean package install'
                }
            }
        }
        }
    }