#!/user/bin/env groovy
@Library('jenkins-shared-library')

def gv

pipeline {   
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        
        stage("build-jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }

        stage("build-image") {
            steps {
                script {
                    buildImage()
                }
            }
        }
        
        stage("deploy") {
            when {
                expression {
                    BRANCH_NAME == "main"
                }
            }
            steps {
                script {
                    echo "Deploying the application"
                }
            }
        }               
    }
}
