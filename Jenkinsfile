pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  triggers {
    cron('@daily')
  }
  stages {
    //Building Images from Dockerfile
    stage('Build') {
      steps {
        sh 'docker build -f "Dockerfile-DB" -t andriyskyy/nextclouddb:latest .'
        sh 'docker build -f "Dockerfile-NC" -t andriyskyy/nc:latest .'
      }
    }
    //Pushing images to public repository
    stage('Publish') {
      steps {
        withDockerRegistry([ credentialsId: "docker-hub", url: "" ]) {
          sh 'docker push andriyskyy/nextclouddb:latest'
          sh 'docker push andriyskyy/nc:latest'
        }
      }
    }
  }
}
