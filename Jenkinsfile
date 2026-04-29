pipeline {
    agent any

    environment {
        APP_NAME = "my-app"
        CONTAINER_NAME = "my-app-container"
        PORT = "3000"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ansari-exe/node-app-cicd-pipeline.git'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $APP_NAME .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $APP_NAME
                '''
            }
        }

        stage('Health Check') {
            steps {
                script {
                    def status = sh(
                        script: "curl -o /dev/null -s -w '%{http_code}' http://localhost:$PORT",
                        returnStdout: true
                    ).trim()

                    if (status != "200") {
                        error "App is not healthy! Status: ${status}"
                    }
                }
            }
        }
    }

    post {
        success {
            mail to: 'mohammadtameem0@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME}",
                 body: "Build successful: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'mohammadtameem0@gmail.com',
                 subject: "FAILED: ${env.JOB_NAME}",
                 body: "Build failed: ${env.BUILD_URL}"
        }
    }
}
