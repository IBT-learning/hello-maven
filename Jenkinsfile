pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
                echo "cloning"
            }
        }
        stage('Verify') {
            steps {
                echo "bokovi is verifying"
            }
        }

        stage('Build') {
                    steps {
                        sh 'mvn compile'
             
                   }
             }
	    
	 // Running sonarqube
        stage('Sonarqube test') { 
            environment {
               scannerHome = tool 'ibt-sonarqube';
            }
            steps {
                withSonarQubeEnv(credentialsId: 'SQ-student', installationName: 'IBT sonarqube') {
                sh "${scannerHome}/bin/sonar-scanner"
              }
            }
        }
	    
stage('Run Test') {
                    steps {
                        sh 'mvn test'
		   
		    }
               }
               stage('upload to artifactory') {
                             steps {
                                 //sh 'mvn test'
                                 configFileProvider([configFile('5d0920bc-97c5-4877-8aa4-2f61975fa9fc')]) {
                                     sh 'mvn package'
                                 }
                             }
                  }

           stage ('OWASP Dependency-Check Vulnerabilities') {
                                steps {
                                    dependencyCheck additionalArguments: '''
                                        -o "./"
                                        -s "./"
                                        -f "ALL"
                                        --prettyPrint''', odcInstallation: 'dependency-check'

                                    dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                                }
                            }
	    
	    stage ('Deploy code to non-prod') {
                steps {
                    script {
                           def remote = [name: 'IBT-Unix', host: '159.223.96.221', user: 'root', allowAnyHosts: true]
                           withCredentials([usernamePassword(credentialsId: " user-bokovi", usernameVariable: 'USERNAME',passwordVariable: 'PASSWORD')]) {
                           remote.password = PASSWORD
                           sshPut remote: remote, from: 'target/hello-maven-1.7-SNAPSHOT.jar', into: '/opt/tomcat/webapps/'
                         }
                }
            }
	 }
    }	
}
