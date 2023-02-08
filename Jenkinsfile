pipeline {
    agent any
    parameters {
        string(name: 'Branch', defaultValue: 'master', description: 'Enter the branch to clone')
        choice
    }
    stages {
        stage('Git clone') {
            steps {
                git branch: '${branch}', changelog: false, credentialsId: 'GitHub-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
            }
        }
        stage('List directories') {
            steps {
               bat 'dir '
            }
        }
        stage('Run mvn commands') {
            steps {
                bat 'source ~/.bash_profile && mvn clean'
                withMaven(maven: 'Maven_3.8.6', mavenSettingsConfig: 'for-Maven') {
                    bat 'mvn clean'
                    }
                }
                }
            }
        }