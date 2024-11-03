pipeline {   
    agent any
    tools {
        maven 'Maven3.9.9'
    }
    stages {
        stage("test") {
            steps {
                script {
                    echo "Executing pipeline for branch $BRANCH_NAME"
                }
            }
        }
        
        stage("build") {
            when {
                expression {
                    BRANCH_NAME == "main"
                }
            }
            steps {
                script {
                    echo "Building the application"
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
