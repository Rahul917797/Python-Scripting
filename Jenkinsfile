pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-hello-app"
        CONTAINER_NAME = "flask-hello-container"
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Rahul917797/Python-Scripting.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME .
                '''
            }
        }

        stage('Deploy Flask App') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true

                docker run -d \
                -p 8085:8085 \
                --name $CONTAINER_NAME \
                $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
