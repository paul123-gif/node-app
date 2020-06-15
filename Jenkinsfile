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
                    def customImage = docker.build("${env.BUILD_ID}")
                    withDockerRegistry([ credentialsId: "Docker-id", url: "https://hub.docker.com/repository/docker/paul1199/node-app" ]) {
      // following commands will be executed within logged docker registry
                    sh 'docker push customImage'
   }
                    }
                }
              }
       
            }
    }
