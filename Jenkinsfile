pipeline{
    agent any
    
    tools {
      maven 'maven3'
    }
    
    environment {
      DOCKER_TAG = getVersion()
    }

    stages{
        stage('SCM'){
            steps{
                echo 'Hello World'
            }
        }
    }
}