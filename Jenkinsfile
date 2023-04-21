pipeline {
    agent any

    stages {
        stage('Git-Clone') {
            steps {
                echo 'cloning'
            }
        }
        stage('Verify') {
            steps {
                bat 'mvn validate'
            }
        }
        stage('Build') {
                    steps {
                        bat 'mvn compile'
                    }
                }
        stage('Sonarqube scan') {
                    steps {
                        bat 'echo performing sonar scans'
                    }
                }
        stage('Run Test') {
                            steps {
                                bat 'mvn test'
                            }
                        }
        stage('Run mvn commands') {
            steps {
            withMaven(maven: 'Maven_3.9.0', mavenSettingsConfig: 'For-Maven') {
                bat 'mvn clean package install deploy'
            }
            }
        }
        }
    }
