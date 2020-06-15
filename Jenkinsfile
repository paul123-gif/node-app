pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
        IMAGE_URL_WITH_TAG = "/node-app:${DOCKER_TAG}"
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t ${IMAGE_URL_WITH_TAG}"
            }
        }
        stage('Docker Push'){
            steps{
                withCredentials([string(credentialsId: 'Docker-id', variable: 'Dockerid')]) {
                    sh "docker login -u paul1199 -p ${Docker-id}"
                    sh "docker push ${IMAGE_URL_WITH_TAG}"
                }
            }
        }
}
    }

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
