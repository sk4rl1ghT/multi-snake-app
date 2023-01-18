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
        stage('Test') {
          steps {
            echo 'Testing...'
            snykSecurity(
              snykInstallation: 'snyk@latest',
              snykTokenId: '57b10bda-3be2-4889-b561-b24c424c3de5',
              // place other optional parameters here, for example:
              additionalArguments: '--all-projects'
            )
          }
        }
        stage('Docker build') {
            steps {
                sh 'docker build -t hiepls98/multi-snake:v1 .'
            }
        }
        stage('Docker push to registry') {
            steps {
                withDockerRegistry(credentialsId: 'docker-hiepls98', url: 'https://index.docker.io/v1/') {
                    sh 'docker push hiepls98/multi-snake:v1'
                }
            }
        }
        stage('Docker Pull Server') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
    }
}
