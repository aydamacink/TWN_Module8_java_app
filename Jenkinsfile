#!/user/bin/env groovy
@Library('jenkins-shared-library')

def gv

pipeline {   
    agent any
    tools {
        maven 'Maven3.9.9'
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
                    buildImage 'dm1984/demo-app:jma-3.0'
                    dockerLogin|()
                    dockerPush 'dm1984/demo-app:jma-3.0'
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
