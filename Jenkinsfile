pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      label 'docker-dind'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: docker
    image: docker:dind
    command: ['cat']
    tty: true
    volumeMounts:
    - name: docker-sock
      mountPath: /var/run/docker.sock
  volumes:
  - name: docker-sock
    hostPath:
      path: /var/run/docker.sock
"""
    }
  }
  stages {
    stage("checkout code"){
        steps {
          checkout scm
        }
    }

    stage('Build Docker image') {
      steps {
        container('docker') {
            sh "ls"
            sh "docker info"
            sh "docker build -t ikmuge/nginx-spa:${BUILD_NUMBER} ."
            sh "docker tag ikmuge/nginx-spa:${BUILD_NUMBER} ikmuge/nginx-spa:latest"
            sh "docker images"          
        }
      }
    }
  }
}
