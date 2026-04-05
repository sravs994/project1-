pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/sravs994/project1-.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t java-app:v1 .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run java-app:v1'
            }
        }

    }
}
