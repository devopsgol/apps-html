pipeline {
    agent {
           label 'slave-devopsgol'
    }
    stages{
        stage("checkout"){
            steps{
                checkout scm
            }
        }
        stage("Build Image"){
            steps{
                sh 'sudo docker build -t web-jomblo-mulu-udah-2024:1.1 .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    sh 'sudo docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                    sh 'sudo docker tag web-jomblo-mulu-udah-2024:1.1 adinugroho251/web-jomblo-mulu-udah-2024:1.1'
                    sh 'sudo docker push adinugroho251/web-jomblo-mulu-udah-2024:1.1'
                    sh 'sudo docker logout'
                }
            }
        }

      stage('Docker RUN') {
          steps {
      	     sh 'sudo docker run -d -p 80 --name web-jomblo-mulu-udah-2024-gagalmaning  adinugroho251/web-jomblo-mulu-udah-2024:1.1'
      }
    }
 }
}
