 pipeline{

	agent {label 'jenkins_agent'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/VarpCode/varpcode-web.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t varpcode/webvarpcode:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push varpcode/webvarpcode:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}