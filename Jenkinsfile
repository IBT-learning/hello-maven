pipeline {
    agent any
    
    parameters {
        string(name:'Branch', defaultValue: 'master', description: ' Enter the branch to clone')
    }

    stages {
        stage('Git clone') {
            steps {
                git branch: '${Branch}', changelog: false, credentialsId: 'Github-login', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
            }
        }
        stage('Verify') {
            steps {
                sh 'ls -lrt'
            }
        }

        stage('Build') {
                    steps {
                        sh 'ls -lrt'
                    }
                }

        stage('Run Test') {
                  // when {
                          // expression {
                                  //  env.BRANCH_NAME == 'master'
                          // }
                   // }
                    steps {
                        sh 'ls -lrt'
                    }
         }
         
        // stage('Run mvn commands') {
           // steps {
              //  withMaven(maven: 'maven_3.8.7', mavenSettingsConfig: 'for-maven') {
                // some block
                  //  sh 'mvn clean package install deploy'
              // }
            //}
        //}
    }
} 
