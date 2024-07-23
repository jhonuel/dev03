pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub')
    }

    stages {
        stage('Verify Docker') {
            steps {
                sh 'docker --version'
                sh 'docker ps'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t jhonuel/dev03:latest .'
            }
        }
        stage('Login') {
            steps {
                script {
                    def dockerhubUser = DOCKERHUB_CREDENTIALS_USR
                    def dockerhubPassword = DOCKERHUB_CREDENTIALS_PSW
                    sh "echo $dockerhubPassword | docker login -u $dockerhubUser --password-stdin"
                }
            }
        }
        stage('Push') {
            steps {
                checkout scmGit(branches: [[name: '*/dev03']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jhonuel/dev03.git']])
                sh 'docker push jhonuel/dev03:latest'
            }
        }
    }
    post {
        always {
            script {
                try {
                    sh 'docker logout'
                } catch (Exception e) {
                    echo "Docker logout failed, likely due to Docker not being available: ${e}"
                }
            }
        }
    }
}
