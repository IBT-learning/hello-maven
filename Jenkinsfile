pipeline {
    agent any

    stages {
        stage('Git-Clone') {
            steps {
                git branch: '${Branch}', changelog: false, credentialsId: 'GitHub-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
                echo 'cloning'
            }
        }
        stage('Verify') {
            steps {
                sh 'mvn validate'
            }
        }
        stage('Build') {
                    steps {
                        sh 'mvn compile'
                    }
                }
        stage('Sonarqube scan') {
                    steps {
                        sh 'performing sonar scans'
                    }
                }
        stage('Run Test') {
                            steps {
                                sh 'mvn test'
                            }
                        }
        stage('Run mvn commands') {
            steps {
            withMaven(maven: 'Maven_3.9.0', mavenSettingsConfig: 'For-Maven') {
                sh 'mvn clean package install deploy'
            }
            }
        }
        }
    }
