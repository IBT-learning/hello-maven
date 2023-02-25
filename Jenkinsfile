pipeline {
    //agent { label 'IBT-UX' }
    agent any

    stages {
        stage('Git clone') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Validate') {
                    steps {
                        sh 'mvn validate'
                    }
                }
        stage('Compile code') {
                            steps {
                                sh 'mvn compile'
                            }
                        }
         stage('Run Tests') {
                             steps {
                                 sh 'mvn test'
                             }
                         }
          stage('Perform SonarQube Analysis') {
           environment {
                      scannerHome = tool 'ibt-sonarqube';
                   }
                steps {
                    withSonarQubeEnv(credentialsId: 'SQ-student', installationName: 'IBT sonarqube') {
                    //sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=dec27-cohort"
                    sh "${scannerHome}/bin/sonar-scanner"
               }
              }
            }
         stage('Create Artifact') {
                             steps {
                                 sh 'mvn package'
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
             stage('Publish Artifact'){
                steps{
                    configFileProvider([configFile(fileId: '5d0920bc-97c5-4877-8aa4-2f61975fa9fc', variable: 'MAVEN_SETTINGS')]) {
                        sh 'mvn deploy -s $MAVEN_SETTINGS'
                    }
                   }
                   }
              stage('Publish Artifactory (withCreds) '){
                    steps{
                        withCredentials([file(credentialsId: 'maven-settings-gunj', variable: 'MAVEN_SETTINGS_XML')]) {
                            sh 'mvn deploy -s $MAVEN_SETTINGS_XML'
                        }

                        }
                    }
               stage('Deploy to Dev'){
                    steps{
                        script{
                             def remote = [name: 'IBT-dev01', host: '178.128.234.201', user: 'root', allowAnyHosts: true]
                             withCredentials([usernamePassword(credentialsId: 'ssh-vm-uname-pwd', passwordVariable: 'password', usernameVariable: 'username')]) {
                                 remote.password = password
                                 sshPut remote: remote, from: 'target/hello-maven-1.3-SNAPSHOT.jar', into: '/opt/tomcat/webapps/'
                             }

                        }

                    }

               }
      }
 }