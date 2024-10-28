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
            script {
                gv.buildJar()
            }
        }

        stage("build image") {
            script {
                gv.buildImage()
            }
        }

        stage("deploy") {
            script {
                gv.deployApp()
            }
        }
    }
}

