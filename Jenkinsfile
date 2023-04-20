pipeline {
    agent any
    parameters {
    string(name:'Branch', defaultValue:'master',description:'Enter the branch to clone')
    }

    stages {
        stage('Git-Clone') {
            steps {
                git branch: '${Branch}', changelog: false, credentialsId: 'GitHub-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
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
                        bat 'performing sonar scans'
                    }
                }
        stage('Run Test') {
                            steps {
                                bat 'mvn test'
                            }
                        }
        //stage('Run mvn commands') {
            //steps {
            //withMaven(maven: 'Maven_3.9.0', mavenSettingsConfig: 'For-Maven') {
                //bat 'mvn clean package install deploy'
            //}
            //}
        //}
        }
    }
