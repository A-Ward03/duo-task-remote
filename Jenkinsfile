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
                docker build -t amward03/duo-deploy-flask:latest -t amward03/duo-deploy-flask:v$BUILD_NUMBER . 
                '''
            }
        }
        stage('pushing images') {
            steps {
                sh '''
                docker push amward03/duo-deploy-flask:latest
                docker push amward03/duo-deploy-flask:v$BUILD_NUMBER
                '''
            }
        }
        stage('deploy') {
            steps {
                sh '''
                kubectl apply -f ./k8s-deployments -n prod
                kubectl rollout restart deployment flask-deployment -n prod
                '''
            }
        }
        stage('clean-up') {
            steps {
                sh '''
                docker system prune -a --force 
                '''
            }
        }
    }
}