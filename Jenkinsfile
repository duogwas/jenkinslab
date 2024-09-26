pipeline{
    agent any
    tools {
      maven 'myMaven'
    }

    stages{
        stage('SCM'){
            steps{
              echo 'Hello world dev'
            }
        }

        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
    }
}