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
            sh 'mvn validate'
        }
        }
        
        stage('Build') {
            steps {
            sh 'mvn compile'
        }
        }


        stage('Sonarqube scan') {
                    environment {
                                   scannerHome = tool 'ibt-sonarqube';
                               }
                              steps {
                                  sh 'echo performing sonar scans'
                                  withSonarQubeEnv(credentialsId: 'SQ-student', installationName: 'IBT sonarqube') {
                                      sh "${scannerHome}/bin/sonar-scanner"
                                  }
                              }
                       }
        
        stage('Run test') {
            steps {
            sh 'mvn test'
            }
        }
        
        stage('Deploy to Artifactory') {
            steps {
            //sh 'mvn test'
                configFileProvider([configFile('5d0920bc-97c5-4877-8aa4-2f61975fa9fc')]) {
                sh 'mvn package'
                //sh 'mvn deploy'
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
            steps  {input 
  message 'Approve to deploy upgrade to production'
}
                    script {
                           def remote = [name: 'IBT-dev', host: '164.92.112.140', user: 'root', allowAnyHosts: true]
                           withCredentials([usernamePassword(credentialsId: "Freda-vmssh", usernameVariable: 'USERNAME',passwordVariable: 'PASSWORD')]) {
                           remote.password = PASSWORD
                           sshPut remote: remote, from: 'target/hello-maven-1.7-SNAPSHOT.jar', into: '/opt/tomcat/webapps/'
                         }
                }        
        }
    }
    }    
}
