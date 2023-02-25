@Library('jenkins-library')_
pipeline {
    agent any 

    stages {
        stage('Run mvn command') { 
            steps {
                sh 'mvn clean package'
            }
        }
      stage('Run SonarScan')
      {
        steps{
          sonarScan()
        }
        
      }
    }
}
