#!/usr/bin/env groovy

pipeline {
	agent {
		docker {
			image 'httpd'
			args '-u root'
		}
	}

	stages {
		stage('Pull') {
			steps {
				checkout scm 
			}
		}
		stage('Build') {
			steps {
				echo 'Building apache server image'
				sh 'docker build -t webserver .' 
			}
		}
		stage('Deploy') {
			steps {
				echo 'Running apache container'
				sh 'docker run -d -p 8082:80 webserver'
			}
		}
	}
}
