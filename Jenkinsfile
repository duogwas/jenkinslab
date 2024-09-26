pipeline{
    agent any
    tools {
      maven 'myMaven'
    }

    stages{
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
    }
}