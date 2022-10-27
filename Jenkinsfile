pipeline {
    agent any
    options {
          timeout(time: 2, unit: 'MINUTES')
      }
    stages {
//         stage('Vadidate maven project') {
//             steps {
//                 sh "mvn validate"
//             }
//         }
//         stage('Run maven test') {
//             steps {
//                 sh "mvn test"
//             }
//         }
//         stage('Run clean install') {
//             steps {
//                 sh "mvn clean install"
//             }
//         }
//         stage('Push package to Jfrog') {
//             steps {
//                 configFileProvider([configFile(fileId: '5d0920bc-97c5-4877-8aa4-2f61975fa9fc', variable: 'MAVEN_SETTINGS_XML')]) {
//                     sh 'mvn -U --batch-mode -s $MAVEN_SETTINGS_XML clean deploy'
//                 }
//             }
//         }
        stage('Configure VM(s) with Tomcat') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    ansiblePlaybook(
                        playbook: 'ansible/tomcat.yaml',
                        inventory: 'ansible/hosts',
                        credentialsId: 'vm-ssh',
                        colorized: true
                        )
                }

            }
        }
        stage('Get Latest Artifacts') {
            steps {
               rtServer (
                  id: 'ibt-artifactory',
                  url: 'https://ibtlearning.jfrog.io/artifactory',
                  // If you're using username and password:
//                   username: 'user',
//                   password: 'password',
                  // If you're using Credentials ID:
                  credentialsId: 'jfrog-jenkins',

              )
              rtDownload (
                  serverId: 'ibt-artifactory',
                  spec: '''{
                        "files": [
                          {
                            "pattern": "ibt-libs-snapshot-local/com/ibt/app/hello-maven/[SNAPSHOT]/hello-maven-[SNAPSHOT].war",

                            "target": "artifacts/"
                          }
                        ]
                  }''',

              )

            }

        }
//         stage('Deploy Code') {
//             steps {
//                ansiblePlaybook(
//                 playbook: 'ansible/deploy-war.yml',
//                 inventory: 'ansible/hosts',
//                 credentialsId: 'vm-ssh',
//                 colorized: true,
//                 extraVars : [
//                       artifact: "/var/lib/jenkins/workspace/peline_feature_master-pipeline_2/target/hello-maven-1.0-SNAPSHOT.war",
//                     ]
//                 )
//             }
//         }
        stage('Deploy to Dev') {
            steps {
               ansiblePlaybook(
                playbook: 'ansible/deploy-war.yml',
                inventory: 'ansible/hosts',
                credentialsId: 'vm-ssh',
                colorized: true,
                extraVars : [
                      artifact: "/var/lib/jenkins/workspace/peline_feature_master-pipeline_2/target/hello-maven-1.0-SNAPSHOT.war",
                      myHosts: "devServer"
                    ]
                )
            }
        }
        stage('Approval') {
            // no agent, so executors are not used up when waiting for approvals
            agent none
            steps {
                script {
                    def deploymentDelay = input id: 'Deploy', message: 'Deploy to production?', submitter: 'ibt-admin', parameters: [choice(choices: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'], description: 'Hours to delay deployment?', name: 'deploymentDelay')]
                    sleep time: deploymentDelay.toInteger(), unit: 'HOURS'
                }
            }
        }
        stage('Deploy to prod') {
            steps {
               ansiblePlaybook(
                playbook: 'ansible/deploy-war.yml',
                inventory: 'ansible/hosts',
                credentialsId: 'vm-ssh',
                colorized: true,
                extraVars : [
                      artifact: "/var/lib/jenkins/workspace/peline_feature_master-pipeline_2/target/hello-maven-1.0-SNAPSHOT.war",
                      myHosts: "prodServer"
                    ]
                )
            }
        }

    }
}
