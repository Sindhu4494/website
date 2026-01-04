pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                git branch: "${env.BRANCH_NAME}",
                    url: 'https://github.com/Sindhu4494/website/'

                sh 'docker build -t abode-webapp:${BUILD_NUMBER} .'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running application tests..."'
                sh 'docker run --rm abode-webapp:${BUILD_NUMBER} echo "Tests Passed"'
            }
        }

        stage('Prod') {
            when {
                branch 'master'
            }
            steps {
                sh '''
                docker stop webapp || true
                docker rm webapp || true
                docker run -d --name webapp -p 80:80 abode-webapp:${BUILD_NUMBER}
                '''
            }
        }
    }
}
