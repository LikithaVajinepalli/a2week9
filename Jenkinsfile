pipeline {
    agent any
    environment {
        DOCKER_USERNAME = "likithavajinepalli"
        DOCKER_PASSWORD = "Likkibala@L?1010"
        IMAGE_NAME = "likithavajinepalli/a2week9"
        IMAGE_TAG = "latest"
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code.."
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image..."
                bat "docker build -t registration-form:latest ."
            }
        }
        stage('Docker Login') {
            steps {
                echo "Logging in to Docker Hub..."
                bat "docker login -u likithavajinepalli -p Likkibala@L?1010"
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
                echo "Pushing Docker Image to Docker Hub..."
                bat "docker push registration-form:v1"
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying application to Kubernetes..."
                bat "kubectl apply -f deployment.yaml --validate=false"
                bat "kubectl apply -f service.yaml"
            }
        }
        stage('Verify Kubernetes Deployment') {
            steps {
                echo "Checking Kubernetes resources..."
                bat "kubectl get deployments"
                bat "kubectl get pods"
                bat "kubectl get services"
            }
        }
    }
    post {
        success {
            echo "PIPELINE COMPLETED SUCCESSFULLY!"
            echo "Docker Image: registration-form:v1"
            echo "Kubernetes deployment completed successfully!"
        }
        failure {
            echo "PIPELINE FAILED!"
            echo "Please check the Jenkins console output."
        }
    }
}