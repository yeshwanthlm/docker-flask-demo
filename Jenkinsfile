pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('amonkincloud-dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -t amonkincloud/flaskapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'sudo docker push amonkincloud/flaskapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'sudo docker logout'
        }
    }
}
