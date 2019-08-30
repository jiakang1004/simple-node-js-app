pipeline {
	agent {
		docker {
			image 'node:10.16.3'
			args '-p 3000:3000 -p 5000:5000'
		}
	}
	environment {
		CI = 'true'
	}
	stages {
		stage('Build') {
			steps {
				sh 'npm install'
			}
		}
		stage('Test') {
			steps {
				sh './scripts/test.sh'
			}
		}
		stage('deliver') {
			steps {
				sh './scripts/deliver-for-development.sh'
				input message: 'Finished using the web site? (Click "Proceed" to continue)'
				sh './scripts/kill.sh'
			}
		}
		// stage('deploy') {
		// 	steps {
		// 		sh './scripts/deploy-for-production.sh'
		// 		input message: 'Finished using the web site? (Click "Proceed" to continue)'
		// 		sh './scripts/kill.sh'
		// 	}
		// }
	}
}