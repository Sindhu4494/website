pipeline {
    agent none

    environment {
        DOCKERHUB_CREDENTIALS = credentials('c7e243d3-d5c1-4596-87ef-bf9af9e72f78')
        IMAGE_NAME = "sindhureddy4494/capstone2:latest"
    }

    stages {

        stage('Hello') {
            agent { label 'Kmaster' }
            steps {
                echo 'Hello World'
            }
        }

        stage('Git Checkout') {
            agent { label 'Kmaster' }
            steps {
                checkout scm
            }
        }

        stage('Docker Build & Push') {
            agent { label 'Kmaster' }
            steps {
                sh '''
                  docker build -t $IMAGE_NAME .
                  echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                  docker push $IMAGE_NAME
                '''
            }
        }

        stage('Kubernetes Deploy') {
            agent { label 'Kmaster' }
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
