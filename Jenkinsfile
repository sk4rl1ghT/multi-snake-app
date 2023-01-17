pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Clone Git') {
            steps {
                checkout scm
            }
        }
        stage('Docker build') {
            steps {
                sh 'docker build -t multi-snake:v1 .'
            }
        }
        stage('Docker push to registry') {
            steps {
                withDockerRegistry(credentialsId: 'docker-hiepls98', url: 'ttps://index.docker.io/v1/') {
                    sh 'docker push multi-snake:v1'
                }
            }
        }
    }
}
