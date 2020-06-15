pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
        DOCKER_URL  = "https://index.docker.io"
        IMAGE_URL_WITH_TAG = "${DOCKER_URL}/node-app:${DOCKER_TAG}"
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
                    sh "docker login -u paul1199 -p ${Docker-id} ${DOCKER_URL}"
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
