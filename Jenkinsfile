/* Scripted pipeline
node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
}*/

// Declarative pipeline

pipeline {
	agent {
		docker {
			image 'maven:3.6.3'
		}
	}
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
				echo "Build"
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	}

	post {
		always {
			echo 'These message will be always shown'
		}
		success {
			echo 'Successfully executed'
		}
		failure {
			echo 'Pipeline failed'
		}
		changed {
			echo 'Pipeline build result has changed since last execution'
		}
	}
}
