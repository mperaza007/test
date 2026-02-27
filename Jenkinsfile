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
                bat 'docker build -t testpipelinejenkins .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker stop testPipeLineJenkins || exit 0
                docker rm testPipeLineJenkins || exit 0
                docker run -d --name testPipeLineJenkins -p 8081:8080 testPipeLineJenkins
                '''
            }
        }
    }
}