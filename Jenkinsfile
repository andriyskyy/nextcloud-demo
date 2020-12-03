pipeline {
  agent { label 'docker' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  triggers {
    cron('@daily')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -f "Dockerfile-DB" -t andriyskyy/NextcloudDB:latest .'
        sh 'docker build -f "Dockerfile-NC" -t andriyskyy/NC:latest .'
      }
    }
    stage('Publish') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry([ credentialsId: "docker-hub", url: "" ]) {
          sh 'docker push andriyskyy/NextcloudDB:latest'
          sh 'docker push andriyskyy/NC:latest'
        }
      }
    }
  }
}
