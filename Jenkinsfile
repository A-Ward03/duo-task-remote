pipeline {
    agent any
    stages {
        stage('this is a test') {
            steps {
                sh '''
                echo "Hello from Jenkins."
                '''
            }
        }
        stage('building images') {
            steps {
                sh '''
                cd nginx 
                docker build -t nginx:latest . 
                cd .. 
                docker build -t amward03/duo-deploy-flask:latest . 
                '''
            }
        }
        stage('pushing images') {
            steps {
                sh '''
                docker push amward03/duo-deploy-flask:latest
                docker push nginx:latest 
                '''
            }
        }
    }
}