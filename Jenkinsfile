pipeline {
    agent any
    stages {
//         stage('Vadidate mavn project') {
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
//         stage('Configure VM(s) with Tomcat') {
//             steps {
//                ansiblePlaybook(
//                 playbook: 'ansible/tomcat.yaml',
//                 inventory: 'ansible/hosts',
//                 credentialsId: 'vm-ssh',
//                 colorized: true
//                 )
//             }
//         }
        stage('Deploy Code') {
            steps {
               ansiblePlaybook(
                playbook: 'ansible/deploy-war.yml',
                inventory: 'ansible/hosts',
                credentialsId: 'vm-ssh',
                colorized: true
                )
            }
        }
    }
}
