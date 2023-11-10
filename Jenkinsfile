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
                    echo "building application"
                    sh "mvn package"
                }
            }
        }

        stage("build image"){
            steps {
                script {
                    echo "building docker image"
                    withCredentials(usernamePassword[credentialsId:"docker", passwordVariable: 'PASS', usernameVariable: 'USERNAME']){
                        sh 'docker build -t brightadams/demo-app:jma-2.0'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push brightadams/demo-app:jma-2.0'
                    }
                }
            }
        }

        stage("Deploy"){
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}