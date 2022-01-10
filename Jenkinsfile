pipeline {

    agent any

    stages {
        
        stage ('removing unupdated refs') {
            steps {
                sh '''
                git --prune=now
               // git remote prune https://github.com/kulabtech/PCF-Repo.git
                git prune
                '''
            }
        }

        stage ('Build') {
            steps {
                withMaven(maven: 'maven_3_5_0') {
                    sh 'mvn clean package'
                }
            }
        }

        stage ('Deploy') {
            steps {

                withCredentials([[$class          : 'UsernamePasswordMultiBinding',
                                  credentialsId   : 'PCF_LOGIN',
                                  usernameVariable: 'USERNAME',
                                  passwordVariable: 'PASSWORD']]) {

                    sh '/usr/local/bin/cf login -a http://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
                    sh '/usr/local/bin/cf push'
                }
            }

        }

    }

}
//gptgpgn,g,,
//telkbpol
