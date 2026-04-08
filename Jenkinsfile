pipeline {
    agent any

    environment {
        IMAGE_NAME = "java-app"
        TAG = "v4"
	MINIKUBE_HOME = "/var/lib/jenkins/.minikube"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/sravs994/project1-.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Load Image to Minikube') {
            steps {
                sh 'MINIKUBE_HOME=/var/lib/jenkins/.minikube minikube image load $IMAGE_NAME:$TAG'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl set image deployment/java-app-deployment \
                java-app-container=$IMAGE_NAME:$TAG
                '''
            }
        }

    }
}
