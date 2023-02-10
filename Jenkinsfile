pipeline {
    agent any

    stages {
        stage('Git clone') {
            steps {
             echo "cloning or clowning"
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
             scannerName = tool 'ibt-sonarqube';
                }
             steps {
               sh 'echo performing sonar scans'
                 withSonarQubeEnv(credentialsId: 'SQ-student', installationName: 'IBT sonarqube') {
               sh "${scannerHome}/bin/sonar-scanner"
                         }
                   }
               }
             }
        stage('Run mvn commands') {
            steps {
                echo "running maven commands.."
                }
            }
        stage('Run Test') {
            steps {
               sh 'mvn test'
                 }
            }
        stage('Upload to artifactory') {
            steps {
              configFileProvider([configFile(fileId: '5d0920bc-97c5-4877-8aa4-2f61975fa9fc', variable: 'MAVEN_SETTINGS_XML')]) {
                sh 'mvn -U --batch-mode -s $MAVEN_SETTINGS_XML clean deploy'
                }
              }
            }
        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
               dependencyCheck additionalArguments: '''
                    -o "./"
                    -s "./"
                    -f "ALL"
                    --prettyPrint''', odcInstallation: 'dependencyCheck'
               dependencyCheckPublisher pattern: 'dependency-check-report.xml'
                   //sh 'mvn deploy'
                 }
               }
        }
    }