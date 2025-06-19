pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/AzazelGod/redis-cluster.git'
      }
    }

    stage('Install dependencies') {
      steps {
        sh '''
          # Установка venv (если ещё нет)
          python3 -m venv venv
          . venv/bin/activate

          # Обновление pip и установка зависимостей
          venv/bin/pip install --upgrade pip
          venv/bin/pip install requests click
        '''
      }
    }

    stage('Deploy Redis Cluster') {
      steps {
        sh '''
          docker-compose down || true
          docker-compose build
          docker-compose up -d
        '''
      }
    }

    stage('Health Check') {
      steps {
        sh '''
          docker ps
          docker exec redis-sentinel redis-cli -p 26379 SENTINEL masters || echo "Check failed"
        '''
      }
    }
  }
}
