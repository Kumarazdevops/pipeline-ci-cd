pipeline {
    agent any
    triggers {
    pollSCM('H/5 * * * *')
}

    stages {
        stage('Checkout') {
            steps {
                git branch : 'main', url: 'https://github.com/Kumarazdevops/pipeline-ci-cd.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build('myimage')
                }
            }
        }
        stage('Test') {
            steps {
                sh 'docker run --rm myimage ./run-tests.sh'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-credentials') {
                        docker.image('myimage').push('latest')
                    }
                }
            }
        }
    }
}
