pipeline {
    agent any
    environment {
        registry = "https://hub.docker.com/repository/docker/paul1199/node-app"
        registryCredential = 'Docker-id'
        
    }
    stages{
        stage('Building our image') {
            steps{
                script {
                    sh "docker build . -t paul1199/node-app:${env.BUILD_ID}"
                    }
                }
              }
        stage('Deploy our image') {
           steps{
                withDockerRegistry([credentialsId: 'Docker-id', url: 'https://hub.docker.com/repository/docker/paul1199/node-app']) {
                    
                    sh "docker push paul1199/node-app:${env.BUILD_ID}"
                }
            }
                   }
            }
    }

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
