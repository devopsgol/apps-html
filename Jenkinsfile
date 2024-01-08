pipeline {
    agent any
    stages{
        stage("checkout"){
            steps{
                checkout scm
            }
        }

        stage("Build Image"){
            steps{
                sh 'sudo docker build -t webserver-devopsgol6969:1.3 .'
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    sh 'sudo docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                    sh 'sudo docker tag webserver-devopsgol6969:1.3 adinugroho251/webserver-devopsgol6969:1.3'
                    sh 'sudo docker push adinugroho251/webserver-devopsgol6969:1.3'
                    sh 'sudo docker logout'
                }
            }
        }

      stage('Docker RUN') {
          steps {
      	     sh 'sudo docker run -d -p 80 --name webserver-degol6969  adinugroho251/webserver-devopsgol6969:1.3'
      }
    }
 }
}
