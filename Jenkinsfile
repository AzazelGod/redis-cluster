pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps { git url: 'https://github.com/AliyunContainerService/redis-cluster.git' }
    }
    stage('Install dependencies') {
      steps {
        sh 'python3 -m pip install --upgrade pip'
        sh 'pip3 install requests click'
      }
    }
    stage('Deploy Redis Cluster') {
      steps {
        sh 'docker-compose down || true'
        sh 'docker-compose build'
        sh 'docker-compose up -d'
      }
    }
    stage('Health Check') {
      steps {
        sh 'docker ps'
        sh 'docker exec redis-sentinel redis-cli -p 26379 SENTINEL masters'
      }
    }
  }
}
