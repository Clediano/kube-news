pipeline {
  agent any

  stages {

    stage ('Build docker image') {
      steps {
        script {
          dockerapp = docker.build("310515/kube-news:v1", "-f ./src/Dockerfile ./src")
        }
      }
    }

  }

}