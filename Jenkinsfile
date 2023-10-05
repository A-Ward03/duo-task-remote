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
                docker build -t amward03/duo-deploy-flask:latest . 
                '''
            }
        }
        stage('pushing images') {
            steps {
                sh '''
                docker push amward03/duo-deploy-flask:latest
                '''
            }
        }
        stage('rolling update') {
            steps {
                sh '''
                kubectl rollout restart deployment flask-deployment
                '''
            }
        }
        stage('retrieve IP') {
            steps {
                sh '''
                kubectl get all
                '''
            }
        }
    }
}