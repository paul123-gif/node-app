pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
        DOCKER_URL  = "https://index.docker.io/"
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
                    sh "docker login -u admin -p ${Docker-id} ${DOCKER_URL}"
                    sh "docker push ${IMAGE_URL_WITH_TAG}"
                }
            }
        }
        #stage('Docker Deploy Dev'){
            steps{
                sshagent(['tomcat-dev']) {
                    withCredentials([string(credentialsId: 'Docker-id', variable: 'Dockerid')]) {
                        sh "ssh ec2-user@172.31.0.38 docker login -u admin -p ${Docker-id} ${DOCKER_URL}"
                    }
					// Remove existing container, if container name does not exists still proceed with the build
					sh script: "ssh ec2-user@172.31.0.38 docker rm -f nodeapp",  returnStatus: true
                    
                    sh "ssh ec2-user@172.31.0.38 docker run -d -p 8080:8080 --name nodeapp ${IMAGE_URL_WITH_TAG}"
                }
            }
        }
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
