pipeline {
    agent any
    environment {
      registry = "salonivichare/poc"	    
      registryCredential = 'dockerhub'
      dockerImage = ''
      HASH = GIT_COMMIT.take(7)
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SaloniVichare1999/poc5.git']]])
                sh 'mvn clean'
                sh 'mvn package'
		sh 'mvn install'
            }
        }
        node('Build docker image'){
            steps{
                script{
			        bat 'docker build -t salonivichare/poc:%HASH% .'
			 }
            }
        }
        stage('Push image to DockerHUB'){
            steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()  
                }
            }
        }
    }
  }
}
