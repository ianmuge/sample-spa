pipeline {
  agent {
    dockerfile {
      filename './Dockerfile'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh '''docker info
docker build -t ikmuge/nginx-spa:${BUILD_NUMBER} .
docker tag ikmuge/nginx-spa:${BUILD_NUMBER} ikmuge/nginx-spa:latest
docker images
'''
      }
    }

  }
}