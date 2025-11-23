pipeline {
    agent any   // run on this Jenkins EC2 itself

    environment {
        IMAGE_NAME     = "node-todo-app"
        CONTAINER_NAME = "node-todo-container"
        APP_PORT       = "8000"
    }

    stages {
        stage('Code Checkout') {
            steps {
                // use YOUR fork URL here
                git url: 'https://github.com/saiyam2805/node-todo-cicd.git', branch: 'master'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Deploy (Run Container)') {
            steps {
                sh """
                docker rm -f ${CONTAINER_NAME} || true
                docker run -d --name ${CONTAINER_NAME} -p ${APP_PORT}:${APP_PORT} ${IMAGE_NAME}:latest
                """
            }
        }
    }
}
