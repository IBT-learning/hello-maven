pipeline {
    agent any
    parameters {
    string(name:'Branch', defaultValue:'master',description:'Enter the branch to clone')
    choice
    }

    stages {
        stage('Git-Clone') {
            steps {
                git branch: '${Branch}', changelog: false, credentialsId: 'GitHub-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
                echo 'Hello World'
            }
        }
        stage('List files') {
            steps {
                bat 'dir'
                echo 'Hi, this is Nnamdi'
            }
        }
        stage('Run mvn commands') {
            steps {
                //bat 'source ~/.bash_profile && mvn clean'
                withMaven(maven: 'Maven_3.9.0', mavenSettingsConfig: 'For-Maven') {
                    bat 'mvn clean'
                }
            }
            }
        }
    }
