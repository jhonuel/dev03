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
                withDockerRegistry([credentialsId: 'dckr_pat_Z8-64RoFuiyPwz0i4INltBSQ5g8', url: '']) {
                    sh 'docker push jhonuel/dev03:"$BUILD_ID"'
                }
            }
        }
    }
}
