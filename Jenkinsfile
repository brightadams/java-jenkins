library identifier: 'custom-lib@master', retriever: modernSCM(
  [$class: 'GitSCMSource',
   remote: 'git@git.mycorp.com:my-jenkins-utils.git',
   credentialsId: 'my-private-key'])_
def gv
pipeline {
    agent any

    tools {
        maven "maven"
    }
    stages {

        stage("build jar"){
            steps {
                script {
                    buildJar()
                }
            }
        }

        stage("build image"){
            steps {
                script {
                    buildImage "brightadams/demo-app:jma-3.0"
                    dockerLogin()
                    dockerPush "brightadams/demo-app:jma-3.0"
                }
            }
        }

        stage("Deploy"){
            steps {
                script {
                    echo "Deploying app"
                }
            }
        }
    }
}
