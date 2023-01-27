pipeline {
  agent any

  stages {

    stage ('Build docker image') {
      steps {
        script {
          dockerapp = docker.build("310515/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
        }
      }
    }

    stage ('Push Docker Image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            dockerapp.push('latest')
            dockerapp.push("${env.BUILD_ID}")
          }
        }
      }
    }

    stage ('Deploy Kubernetes') {
      steps {
        withCubeconfig([credentialsId: 'kubeconfig']) {
          sh 'kubectl apply -f ./k8s/deployment.yaml'
        }
      }
    }

  }
}