pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  triggers {
    cron('@daily')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -f "Dockerfile-DB" -t andriyskyy/nextclouddb:latest .'
        sh 'docker build -f "Dockerfile-NC" -t andriyskyy/nc:latest .'
      }
    }
    stage('Publish') {
      steps {
        withDockerRegistry([ credentialsId: "docker-hub", url: "" ]) {
          sh 'docker push andriyskyy/NextcloudDB:latest'
          sh 'docker push andriyskyy/NC:latest'
        }
      }
    }
  }
}
