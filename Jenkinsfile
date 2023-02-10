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
        stage('Compile') {
            steps {
                sh 'mvn compile'
                    }
                }
        stage('Package') {
            steps {
                sh 'mvn package'
                    }
                }
          stage('Install') {
                    steps {
                       sh 'mvn install'
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

        stage('Run Test') {
                    steps {
                        sh 'mvn test'
                    }
         }
         stage('upload to artifactory') {
                             steps {
                                 //sh 'mvn test'
                                 configFileProvider([configFile(fileId: '5d0920bc-97c5-4877-8aa4-2f61975fa9fc', variable: 'MAVEN_SETTINGS_XML')]) {
                                     sh 'mvn -U --batch-mode -s $MAVEN_SETTINGS_XML clean deploy'
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
                           def remote = [name: 'tomcat-dev', host: '147.182.164.39', user: 'root', allowAnyHosts: true]
                           withCredentials([usernamePassword(credentialsId: 'Fancy', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                           remote.password = PASSWORD
                           sshPut remote: remote, from: 'target/hello-maven-2.2.0-SNAPSHOT.jar', into: '/opt/tomcat/webapps/'
                         }
                }
            }
        }
    }
}