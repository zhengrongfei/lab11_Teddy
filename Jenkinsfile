pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
       sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('K8s') {
      steps {
        sh 'kubectl set image cocozheng/teddy container-name=image-id'
} }
} }
