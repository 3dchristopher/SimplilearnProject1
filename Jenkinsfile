#!/usr/bin/env groovy

pipeline {
	agent {
		docker {
			image 'httpd'
			args '-u root'
		}
	}

	stages {
		stage('Build') {
			steps {
				echo 'Building apache server image'
				sh 'docker build -t webServer .' 
			}
		}
		stage('Deploy') {
			steps {
				echo 'Running apache container'
				sh 'docker run -d -p 8082:80 webServer'
			}
		}
	}
}
