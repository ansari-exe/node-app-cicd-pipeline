pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f node-app-container || true'
                sh 'docker run -d -p 3000:3000 --name node-app-container node-app'
            }
        }
    }
}
