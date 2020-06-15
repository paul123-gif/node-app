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
                    sh "docker build . -t ${env.BUILD_ID}"
                    }
                }
              }
        stage('Deploy our image') {
           steps{
                withCredentials([string(credentialsId: 'registryCredential', variable: 'dockerPwd')]) {
                    sh "docker login -u paul1199 -p ${dockerPwd}"
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
