pipeline {
    agent any

    stages {
        stage('Fix Permissions') {
            steps {
                sh 'chmod +x ./mvnw'
            }
        }
        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot-k8s:latest .'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
