@Library('jenkins-library')_
pipeline {
    agent any 

    stages {
        
        stage('mvn install') { 
            steps {
                sh "mvn clean install"
            }
        }
        
        stage('mvn install') { 
            steps {
                script {
                    
                    printBuildinfo()
                    
                }
            }
        }
        
        stage('Deploy using Jenkins Library') { 
            steps {
                script {
                    
                    deployTomcat()
                    
                }
            }
        }
        stage('Test Blasie Deploy Script') { 
            steps {
                script {
                    
                    deploy()
                    
                }
            }
        }
    }
}
