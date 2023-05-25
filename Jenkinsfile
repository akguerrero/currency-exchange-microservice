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
	agent any
	stages {
		stage('Build') {
			steps {
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
			'Pipeline build result has changed since last execution'
		}
	}
}
