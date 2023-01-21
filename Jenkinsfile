@Library('jenkins-library')_
pipeline {
    agent any 

    stages {
        
        stage('Run mvn command') { 
            steps {
                mvn_commands()
            }
        }
        
        stage('Test script') { 
            steps {
                script {
                    
                    printBuildinfo {
        name = "Sample Name"
    }
                    
                }
            }
        }
        
        stage('Get Timestamp') { 
            steps {
                script {
                    
                    def TIMESTAMP = getTimeStamp();
                    echo "${TIMESTAMP}"
                    
                }
            }
        }
    }
}
