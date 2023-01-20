pipeline {
    agent any
    environment {
      registry = "salonivichare/poc"	    
      registryCredential = 'Dockerhub'
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
        stage('Docker Build') {
		steps {
			sh docker.build("my-image:${env.BUILD_ID}\n
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
