pipeline {
    agent any
    environment {
        registry = "https://hub.docker.com/repository/docker/paul1199/node-app"
        registryCredential = 'Docker-id'
        dockerImage = ''
    }
    stages{
        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build -t registry + ":$BUILD_NUMBER"
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
