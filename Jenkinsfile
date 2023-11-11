pipeline {
    agent any

    tools {
        maven "maven"
    }
    stages {

        stage("incrementing version"){
            steps {
                script {
                    //we increment the mvn package version
                    echo "Increasing version"
                    sh "mvn build-helper:parse-version versions:set -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} versions:commit"
                    //use regex to search for the version tag in pom.xml
                    def matcher = readFile("pom.xml") =~ '<version>(.+)</version>'
                    //get the children text of the tag
                    def version = matcher[0][1]
                    //append the build number(number of builds in jenkins) to the version which we store in an env variable so we can use it as docker image tags..
                    env.IMAGE_VERSION = "$version-$BUILD_NUMBER"
                }
            }
        }

        stage("build jar"){
            steps {
                script {
                    echo "building application"
                    //mvn clean package will clear every jar file in the /target folder before building a new one..
                    sh "mvn clean package"
                }
            }
        }

        stage("build image"){
            steps {
                script {
                    echo "building docker image"
                    withCredentials([usernamePassword(credentialsId:"docker", passwordVariable: 'PASS', usernameVariable: 'USER')]){
                        sh "docker build -t brightadams/demo-app:jma-${IMAGE_VERSION} ."
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh "docker push brightadams/demo-app:jma-${IMAGE_VERSION}"
                    }
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