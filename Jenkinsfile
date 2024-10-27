def gv

pipeline {   
    agent any
    
stages {
        stage("build") {
            steps {
		echo 'building the application'
            }
        }
        stage("test") {
            steps {
                steps{
                    echo 'testing the application'

                }
            }
        }

        stage("deploy)" {
            steps {
                echo 'deploying the application'
                }
            }
        }

    }
