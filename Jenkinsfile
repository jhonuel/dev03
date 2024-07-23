pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('jenkins-pwd-01') // Aquí debes usar el ID de tus credenciales de Docker Hub
    }

    stages {
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
                sh 'docker push jhonuel/dev03:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
