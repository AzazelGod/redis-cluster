pipeline {
  agent any

  stages {
    stage('Clone') {
      steps {
        git url: 'https://github.com/AliyunContainerService/redis-cluster.git'
      }
    }

    stage('Deploy Redis Cluster') {
      steps {
        dir('redis-cluster') {
          sh 'ls -l'  // Для отладки — проверить, что есть в папке
          sh 'docker-compose up -d --build'
        }
      }
    }
  }
}
