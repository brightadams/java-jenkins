pipeline {
    agent any
    stages {
        stage("Test"){
            steps {
                echo "Testing app"
            }
        }

        stage("Build"){
            steps {
                echo "Building app"
            }
        }

        stage("Deploy"){
            environment {
                //so this will export these variables in your jenkins container terminal so it can be used for the aws authentication so kubectl can execute to the cluster
                AWS_ACCESS_KEY_ID = credentials("jenkins-aws-access-key")
                AWS_SECRET_ACCESS_KEY = credentials("jenkins-aws-secret-key")
            }
            steps {
                echo "Deploying app"
                //
                sh "kubectl create deployment nginx-depl --image=nginx"
            }
        }
    }
}
