pipeline {
    agent any


    stages {
        stage('Git clone') {
            steps {
                git branch: 'gunj-app', changelog: false, credentialsId: 'GitHub-creds', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
            }
        }
        stage('Verify') {
            steps {
                sh 'ls -lrt'
                sh 'echo "building ${VERSION}" '
                sh 'echo buiding ${VERSION}'
            }
        }
        stage('Run Test') {
                    steps {
                        sh 'ls -lrt'
                        withCredentials([usernamePassword(credentialsId: 'GitHub-creds', passwordVariable: 'password', usernameVariable: 'username')]) {
                            sh 'echo ${username}'
                        }
                    }
         }
         stage('Run mvn commands') {
            steps {
                //sh 'source ~/.bash_profile && mvn clean'
                withMaven(maven: 'Maven_3.8.6', mavenSettingsConfig: 'for-Maven') {
                    sh 'mvn clean'
                }
            }
            }
        }
    }
