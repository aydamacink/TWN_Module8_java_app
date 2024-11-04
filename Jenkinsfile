pipeline {   
    agent any
    tools {
        maven 'Maven3.9.9'
    }
    stages {
        stage("increment version") {
            steps {
                script {
                    echo "incrementing app version"
                    // Run Maven commands to set the new version using Maven's exec plugin to calculate the new version internally
                    sh '''
                        mvn build-helper:parse-version versions:set \
                            -DnewVersion=$(mvn -q \
                                -Dexec.executable="echo" \
                                -Dexec.args='${parsedVersion.majorVersion}.${parsedVersion.minorVersion}.${parsedVersion.nextIncrementalVersion}' \
                                org.codehaus.mojo:exec-maven-plugin:1.3.1:exec) versions:commit
                    '''

                    // Read the updated version from pom.xml to set as the Docker image tag
                    def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                    def version = matcher[0][1]
                    env.IMAGE_NAME = "$version-$BUILD_NUMBER"
                }
            }
        }
        
        stage("build app") {
            steps {
                script {
                    echo "Building the application"
                    sh 'mvn clean package'
                }
            }
        }

        stage("build image") {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "docker build -t dm1984/demo-app:${env.IMAGE_NAME} ."
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh "docker push dm1984/demo-app:${env.IMAGE_NAME}"
                    }
                }
            }
        }
        
        stage("deploy") {
            steps {
                script {
                    echo "Deploying the application"
                }
            }
        }               
    }
}
