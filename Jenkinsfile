pipeline {
    agent any
    triggers {
    pollSCM('H/5 * * * *')
}

    stages {
        stage('Checkout') {
            steps {
                git branch : 'feature/updates', url: 'https://github.com/Kumarazdevops/pipeline-ci-cd.git'
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
                echo "Pass test"
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('', 'sravankumar0338') {
                        docker.image('myimage').push('latest')
                    }
                }
            }
        }
    }
}
