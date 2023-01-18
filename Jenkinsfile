pipeline {
    agent any
    parameters {
        string(name:'Branch', defaultValue:'master', description:'Enter the branch to clone')
    }

    stages {
        stage('Git clone') {
            steps {
                git branch: '${Branch}', changelog: false, credentialsId: 'GitHub-creds', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
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
        when {
            expression {
                env.BRANCH_NAME == 'master'
            }
        }
                    steps {
                        sh 'ls -lrt'
                    }
         }
         stage('Run mvn commands') {
            steps {
                withMaven(maven: 'Maven_3.8.6', mavenSettingsConfig: 'for-Maven') {
                    sh 'mvn clean'
                }
            }
            }
        }
    }
