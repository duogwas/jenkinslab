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

          stage('Docker Deploy'){
            steps{
              ansiblePlaybook credentialsId: 'dev-server-248', disableHostKeyChecking: true, extras: "-e DOCKER_TAG=${DOCKER_TAG}", installation: 'ansible', inventory: 'dev.inv', playbook: 'deploy-docker.yml'
            }
        }
    }
}

def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}