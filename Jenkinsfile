pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'printenv'
                sh 'docker build -t jhonuel/test:"$BUILD_ID" .'
            }
        }
        stage('Publish') {
            steps {
                withDockerRegistry([credentialsId: '', url: '']) {
                    sh 'docker push jhonuel/test:"$BUILD_ID"'
                }
            }
        }
    }
}
