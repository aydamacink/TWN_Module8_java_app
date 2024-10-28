def gv

pipeline {   
    agent any
    tools {
        maven 'Maven3.9.9'
    }
    
    stages {
        stage("init"){
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        
        stage("build jar") {
            steps {
                echo 'building the application'
                sh 'mvn package'
            }
        }

        stage("build image") {
            steps {
                echo 'building the docker image'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                    sh 'docker build -t dm1984/demo-app:jma-2.0 .'
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push dm1984/demo-app:jma-2.0'
                }
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application'
            }
        }
    }
}

