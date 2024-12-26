pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('tall-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/tallahmad047/nodejsdemo.git'
            }
        }
        stage('Build docker image') {
            steps {  
                bat 'docker build -t tallahmad/nodetest:%BUILD_NUMBER% .'
            }
        }
        stage('login to dockerhub') {
            steps {
               // bat 'echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin'
                bat '''
                    echo %DOCKERHUB_CREDENTIALS_PSW%| docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin
                '''
            }
        }
        stage('push image') {
            steps {
                bat 'docker push tallahmad/nodetest:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}