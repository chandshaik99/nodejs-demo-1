pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('ndlchand-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/chandshaik99/nodejs-demo-1.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t ndlchand/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push ndlchand/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

