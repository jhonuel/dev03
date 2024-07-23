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
                withDockerRegistry([credentialsId: 'jenkins-pwd-01', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push jhonuel/dev03:"$BUILD_ID"'
                }
            }
        }
    }
}
