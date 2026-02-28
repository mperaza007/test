pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'jdk-21'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
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
                bat 'docker build -t test-pipe-line-jenkins .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker stop test-pipe-line-jenkins || exit 0
                docker rm test-pipe-line-jenkins || exit 0
                docker run -d --name test-pipe-line-jenkins -p 8081:8080 test-pipe-line-jenkins
                '''
            }
        }
    }
}