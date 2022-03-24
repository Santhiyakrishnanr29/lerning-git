pipeline {
  environment {
    imagename = "santhiyaradhakrishnan/mynginxapp"
    registryCredential = 'santhiyaradhakrishnan(dockerhub token)'
    dockerImage = ''
    }
    agent any
    stages {
        stage('Git Clone') {
            steps {
                git([url: 'https://github.com/Santhiyakrishnanr29/lerning-git.git', branch: 'master', credentialsId: 'Santhiyakrishnanr29(github token)'])
            }
        }
        stage('Build Image') {
            steps {
               script {
                 dockerImage = docker.build imagename
               }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                  docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                  }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps {
              sh "docker rmi $imagename:$BUILD_NUMBER"
             }
        }
    }
}
