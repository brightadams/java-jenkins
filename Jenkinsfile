@Library("jenkins-shared-library@main")_
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