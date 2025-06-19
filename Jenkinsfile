pipeline {
  agent any

  stages {
    stage('Clone repo') {
      steps {
        git url: 'https://github.com/AzazelGod/redis-cluster.git'
      }
    }
    stage('Deploy Redis Cluster') {
      steps {
        sh 'docker-compose up -d --build'
      }
    }
  }
}
