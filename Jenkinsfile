pipeline {
    agent any
    parameters{
        string(name:'Branch', defaultvalue:'master', description:'Enter the branch to cloene')
    }    

    stages {
        stage('Git clone') {
            steps {
                git branch: '${Branch}', changelog: false, credentialsId: 'for-github', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
            }
        }
        stage('List files') {
            steps {
                sh 'ls -lrt'
            }
        }
        stage('Run mvn commands') {
            steps {
                //sh 'source ~/.bash_profile && mvn clean'
                withMaven(maven: 'Maven_3.8.6', mavenSetingsConfig: 'For Maven')
            }
        }
    }
}
