pipeline {
	agent any
	environment {
		IMAGE_NAME='dockerlearnsrikanth/jenkins-flask-app'
		IMAGE_TAG='${IMAGE_NAME}:${env.GIT_COMMIT}'
	}

	stages {

	  stage('SETUP') {
	      steps {
	                       
	      	sh '''
		sudo yum install python3-pip -y
		pip install -r requirements.txt

		'''

		}
	      }

	  stage('TEST') {
		steps{
		  sh "pytest"
		}
	     }
	  stage('DOCKER_LOGIN'){
	  	steps{
		 withCredentials([usernamePassword(credentialsId: 'docker-creds', 
		 passwordVariable: 'dkr-password', usernameVariable: 'dkr-username')]) {
    	         sh "echo ${dkr-password} | docker login -u ${dkr-username} --password-stdin"
			}
		 echo " Docker login successful"
		}
	    }   
	 stage('DOCKER_IMAGE_BUILD'){
	 	steps{
		   sh " docker build -t ${IMAGE_TAG} ."
		   echo " docker build image successful"
		   sh " docker images "

		}

	}
	
	stage('DOCKER_IMAGE_PUSH'){
                steps{
                   sh " docker push ${IMAGE_TAG} ."
                   echo " docker push image successful"
                	}
        	}
	}
}
	



















