#!/user/bin/env groovy
library identifier:'jenkins-shared-library@main', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://github.com/aydamacink/twn_module_8_jenkins_shared_Library.git', 
    credentialsId: 'github-credentials'
    ]
)

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
                    // Create an instance of Docker with `this` as the script reference
                    def docker = new com.example.Docker(this)

                // Use the `Docker` methods directly
                buildImage 'dm1984/demo-app:jma-3.0'
                docker.dockerLogin()
                docker.dockerPush 'dm1984/demo-app:jma-3.0'
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
