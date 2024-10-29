pipeline {   
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application"
                    echo "Executing pipeline for branch $BRANCH_NAME"
                }
            }
        }
        stage("build") {

            steps {
                when{
                    expression {
                        BRANCH_NAME=="main"
                    }
                }
                script {
                    echo "Building the application"
                }
            }

        stage("deploy") {
            steps {
                when{
                    expression {
                        BRANCH_NAME=="main"
                    }
                }
                script{
                    echo "deploying the application"
                }
            }
        }               
    }
} 
