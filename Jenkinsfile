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
                sh 'sudo docker build -t webserver-devopsgol6969:1.0 .'
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    sh 'sudo docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                    sh 'sudo docker tag webserver-devopsgol6969:1.0 adinugroho251/webserver-devopsgol6969:1.0'
                    sh 'sudo docker push adinugroho251/webserver-devopsgol6969:1.0'
                    sh 'sudo docker logout'
                }
            }
        }

      stage('Deploying Node App to K8S') {
          steps {
               withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'kubernetes-devopsgol', namespace: 'default', serverUrl: 'https://10.20.30.40']]) {
                   sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'
                   sh 'chmod u+x ./kubectl'
                   sh "./kubectl get ns"
                   sh "./kubectl apply -f html-nginx.yaml"
                   
      }
    }
 }
 }
}    
