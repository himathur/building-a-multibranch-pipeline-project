pipeline{
	agent {
		docker {
			image 'node:6-alpine'
			args '-p 3000:3000 -p 5000:5000'
		}
	}
	environment {
		CI = 'true'
	}

	stages {
		stage ('Build') {
			steps {
				sh 'npm install'
			}
		}
		stage ('Test') {
			steps {
				sh './jenkins/scripts/test.sh'
			}
		}

		stage('Deploy for development') {
			when {
				branch 'development'
			}
			steps {
				sh './jenkins/scripts/deliver-for-development.sh'
				input message : 'Finshed using the web site? (Click proceed to continue)'
				sh  './jenkins/scripts/kill.sh'
			
			}
		}

	}
}