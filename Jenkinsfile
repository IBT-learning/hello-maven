pipeline {
    agent any 
    stages {  
        stage('Vadidate mavn project') { 
            steps {
                sh "mvn validate"
            }
        }
        stage('Run maven test') { 
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    sh "mvn test"
                }
                
            }
        }
        stage('Run clean install') { 
            steps {
                echo "Unit Test Complete"
            }
        }
        stage('Push package to Registry') { 
            steps {
                configFileProvider([configFile(fileId: '5d0920bc-97c5-4877-8aa4-2f61975fa9fc', variable: 'MAVEN_SETTINGS_XML')]) {
                    sh 'mvn -U --batch-mode -s $MAVEN_SETTINGS_XML clean deploy -DskipTests=true'
                }
            }
        }
    }
}
