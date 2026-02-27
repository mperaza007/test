pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'jdk-21'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/cicd-demo.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t cicd-demo .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker stop cicd-demo || exit 0
                docker rm cicd-demo || exit 0
                docker run -d --name cicd-demo -p 8081:8080 cicd-demo
                '''
            }
        }
    }
}