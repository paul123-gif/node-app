pipeline {
    agent any
    environment {
        
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
                withDockerRegistry([credentialsId: 'Docker-id']) {
                    
                    sh "docker push :${env.BUILD_ID}"
                }
            }
                   }
            }
    }
