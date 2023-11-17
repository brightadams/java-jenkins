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
            steps {
                echo "Deploying app
            }
        }
    }

    post {
        always {
            echo "always renders"
        }

        success {
            echo "renders on success"
        }

        failure {
            echo "renders on failure"
        }
        //
    }
}
