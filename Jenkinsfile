pipeline {
  agent any
  
    stages {

      stage('Push') {
        steps {
          withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
            /* Push images to dockerhub*/
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
            sh "docker push awfullycold/service-go"
            sh "docker push awfullycold/service-dotnet"
          }
        }
      }  	

      stage('Docker Build') {
        steps {
          /* Build image with docker*/
          sh "docker build -t hepsitech/service-go:latest ."
          sh "docker build -t hepsitech/service-dotnet ."
        }
      }


      stage('Deploy Go app') {
        steps {
            sh 'kubectl apply -f service.yaml'
        }
      }

      stage('Deploy Dotnet app') {
        steps {
            sh 'kubectl apply -f service.yaml'
        }
      }


  }

}