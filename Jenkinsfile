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
                sh 'docker push hiepls98/multi-snake:v1'
            }
        }
    }
}
