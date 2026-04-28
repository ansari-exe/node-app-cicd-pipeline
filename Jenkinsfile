pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/ansari-exe/node-app-cicd-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:3000 node-app'
            }
        }
    }
}
