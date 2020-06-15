pipeline {
    agent any
    environment {
        registry = "https://hub.docker.com/r/docker/paul1199/node-app"
        registryCredential = 'Docker-id'
        dockerImage = ''
    }
    stages{
        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
              }
        stage('Deploy our image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                        }
                       }
                    }
                   }
            }
    }

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
