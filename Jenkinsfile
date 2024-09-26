pipeline{
    agent any

    tools {
      maven 'myMaven'
    }

    environment {
      DOCKER_TAG = getVersion()
    }

    stages{
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }

        stage('Docker Build'){
            steps{
                sh "docker build . -t duogwas/multibranchapp:${DOCKER_TAG}"
            }
        }

        stage('DockerHub Push'){
          steps{
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                    sh "docker login -u duogwas -p ${dockerHubPwd}"
                }
                sh "docker push duogwas/multibranchapp:${DOCKER_TAG}"
              }
        }
    }
}

def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}