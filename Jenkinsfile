pipeline {
agent any 

   stages {

    stage('Cloning Git') {

      steps
        {
        /* Let's make sure we have the repository cloned to our workspace */
       git credentialsId: 'snakedemo', url: 'https://github.com/sk4rl1ghT/multi-snake-app.git'
       checkout scm
        }  
    }
    stage('SAST'){
      steps{
        sh 'echo SAST stage'
       }
    }

    
    stage('Build-and-Tag') {
      steps{    
	 withDockerRegistry(credentialsId: 'docker account', url: 'https://index.docker.io/v1/') {
	     sh label: ", script:'docker build -t hiepls98/multi-snake:v1 .'   
	     sh label: ", 'docker push hiepls98/multi-snake:v1 '
	   }
      }
    }

    stage('Post-to-dockerhub') {
     steps {
        sh 'echo Post to dockerhub'
     }
    }

    stage('SECURITY-IMAGE-SCANNER'){
      steps {
        sh 'echo scan image for security'
     }
    }

    stage('Pull-image-server') {
      steps {
         sh 'echo pulling image ...'
       }
      }
    
    stage('DAST') {
      steps  {
         sh 'echo dast scan for security'
        }
    }
 }
}
