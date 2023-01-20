pipeline {
    agent any
    environment {
      registry = "salonivichare/poc"
      registryCredential = 'dockerhub'
      dockerImage = ''
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
        stage('Build docker image'){
            steps{
                //script{
			        //dockerImage = docker.build registry + ":$BUILD_NUMBER"
				sh 'docker build -t salonivichare/poc:$BUILD_NUMBER 
			 //}
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
