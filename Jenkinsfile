pipeline {
    agent any
   // parameters {
     //   string(name:'Branch', defaultValue:'master', description:'Enter the branch name')
       // choice(name:'Food', choices:['ice-cream','chocolate','cook-meal'], description:'choose')
       //}

       stages {
        stage('Git clone') {
            steps {
       //         git branch: '${Branch}', changelog: false, credentialsId: 'for-github', poll: false, url: 'https://github.com/IBT-learning/hello-maven.git'
                  echo 'cloning'
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
           stage('DevOps') {
            steps {
             echo 'DevOps is more like a cultural shift to modern-day organizations. It enhances collaboration between development and operations team as well as improves cost management'
            }
        }
             stage('Arsenal') {
            steps {
             echo 'Arsenal is the best soccer team in the world at the moment'
            }
        }
            stage('Jenkins Email') {
            steps {
            emailext body: '''Greetings,

This is Daniel Bundor, a DevOps Engineer in Training at IBT-Learning. Please be aware that this is a practice email. I look forward to hearing from you. Thank you.

Best regards,''', subject: 'Jenkins Email', to: 'cbundor91@gmail.com'
            }
        }
             stage('My Intro') {
            steps {
             echo 'Daniel Bundor is a DevOps Engineer in training at IBT-Learning. He is very interested in bringing value to the DevOps community and that\'s why he has decided to spent more time developing his job-ready skills while having fun.'
            }
        }
          stage('IBT-Learning') {
            steps {
             echo 'IBT-Learning is doing a very great job developing DevOps Engineers for the future. I am personally having a great time learning DevOps at IBT-Learning. Our Nov15th Co-Hort started with Adrian; an amazing guy who taught us Linux Fundamentals and Python. We are now with Gunjan; an experienced agile professional who has taught us version control using Git and GitHub, Maven; a Java project\'s build and management tool, Artifactory; a JFrog binary repository manger, and we are now learning Jenkins; an open source automation server that helps with building, testing, and deploying as well as facilitating continuous integration and continuous delivery, after which we will move onto Ansible (at the moment of this file edit)'
            }
        }
         stage('Run Test') {
        // when {
          //   expression {
            //      env.BRANCH_NAME == 'master'
             //}
          //}

             steps {
                       sh 'ls -lrt'
                    }
                }
                 stage('Run mvn commands') {
                            steps {
                              //sh '~/.zshrc && mvn clean'
                             // withMaven(maven: 'Maven_3.8.7', mavenSettingsConfig: 'for-Maven') {
                              //sh 'mvn clean validate test install package deploy'
                              echo 'running maven commands'
                            }
                 }

        }
    }
}