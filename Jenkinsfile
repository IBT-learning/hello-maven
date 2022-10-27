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
        stage('Get Latest Artifacts') {
            steps {
               sh '''
               # Artifactory location
               server=https://ibtlearning.jfrog.io/artifactory
               repo=ibt-libs-snapshot-local

               # Maven artifact location
               name=hello-maven
               artifact=com/ibt/$name
               path=$server/$repo/$artifact
               version=$(curl -s $path/maven-metadata.xml | grep latest | sed "s/.*<latest>([^<]*)</latest>.*/1/")
               build=$(curl -s $path/$version/maven-metadata.xml | grep '<value>' | head -1 | sed "s/.*<value>([^<]*)</value>.*/1/")
               war=$name-$build.war
               url=$path/$version/$war

               # Download
               echo $url
               wget -q -N $url

               '''
            }
        }
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

//         stage('Get Latest Artifacts') {
//             steps {
//                sh '''
//                # Artifactory location
//                server=https://ibtlearning.jfrog.io/artifactory
//                repo=snapshot
//
//                # Maven artifact location
//                name=hello-maven
//                artifact=com/ibt/$name
//                path=$server/$repo/$artifact
//                version=$(curl -s $path/maven-metadata.xml | grep latest | sed "s/.*<latest>([^<]*)</latest>.*/1/")
//                build=$(curl -s $path/$version/maven-metadata.xml | grep '<value>' | head -1 | sed "s/.*<value>([^<]*)</value>.*/1/")
//                war=$name-$build.war
//                url=$path/$version/$war
//
//                # Download
//                echo $url
//                wget -q -N $url
//
//                '''
//             }
//         }
    }
}
