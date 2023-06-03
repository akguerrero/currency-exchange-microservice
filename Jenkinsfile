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
	//agent {docker {image 'maven:3.6.3'}}
	agent any
	environment {
		dockerHome = tool 'MyDocker'
		mavenHome = tool 'MyMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker --version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compile') {
			steps {
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps {
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps {
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Package') {
			steps {
				sh 'mvn package -DskipTests'
			}
		}
		stage('Package') {
			steps {
				sh 'mvn package -DskipTests'
			}
		}
		stage('Build Docker Image') {
			steps {
				//sh "docker build -t akguerrerok/currency-exchange-devops:${env.BUILD_TAG}"
				script {
					dockerImage = docker.build("akguerrerok/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				//sh "docker push akguerrerok/currency-exchange-devops:${env.BUILD_TAG}"
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
		}
	}

	post {
		always {
			echo 'This message will always be shown'
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
