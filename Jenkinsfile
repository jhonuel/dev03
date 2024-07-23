pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'printenv'
                sh 'docker build -t jhonuel/dev03:"$BUILD_ID" .'
            }
        }
        stage('Publish') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push jhonuel/dev03:"$BUILD_ID"'
                }
            }
        }
    }
}
