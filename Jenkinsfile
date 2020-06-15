pipeline {
    agent any
    environment {
        registry = "https://hub.docker.com/repository/docker/paul1199/kubernetes"
        registryCredential = 'Docker-id'
        
    }
    stages{
        stage('Building our image') {
            steps{
                script {
                    def customImage = docker.build(:${env.BUILD_ID}")
                    customImage.push()
                    }
                }
              }
        stage('Deploy our image') {
           steps{
                withDockerRegistry([credentialsId: 'Docker-id']) {
                    
                    sh "docker push :${env.BUILD_ID}"
                }
            }
                   }
            }
    }
