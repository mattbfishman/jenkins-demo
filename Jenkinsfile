pipeline {
    agent any 

	  environment {
		    DOCKERHUB_CREDENTIALS = credentials('docker-creds')
	  }

    stages {
        stage('Build') { 
            agent any 
            steps {
                echo 'Building Image from Dockerfile'
                echo 'Will tag the image as test-jenkins. Will need this for push stage.'
                sh 'docker build -t test-jenkins dockerfiles/jupytertravis/.'
                echo 'Build Stage Complete'
            }
        }
      
        stage('Test') { 
            agent any
            steps {
                echo 'No test is being performed. Shown for demo purposes.'
                echo 'Test Stage Complete'
            }
        }
        stage('Docker Login') {
            steps {
                echo 'Use Docker Hub credentials stored in Jenkins.'
			        	sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                echo 'Docker Login Stage Complete'
			      } 
        }

        stage('Push Image') {
			      steps {
                echo 'Pushing image to Docker Hub'
                sh 'docker images'
                sh 'docker tag test-jenkins mbfishman94/build-pipeline-demo'
				        sh 'docker images'
                sh 'docker push mbfishman94/build-pipeline-demo:latest'
                echo 'Push Stage Complete'
			}
		}

    }
}