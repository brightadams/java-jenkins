pipeline {
    agent any
    stages {
        stage("init"){
            steps {
                gv = load "script.groovy"
            }
        }
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
            steps {
                echo "Deploying app"
            }
        }
    }
}
