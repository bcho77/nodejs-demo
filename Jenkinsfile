pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('vaninoel')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/bcho77/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'sudo docker build -t vaninoel/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'sudo docker push vaninoel/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

