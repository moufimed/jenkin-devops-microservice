//Declarative
pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3'}}
	environment {
		dockeHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage ("Build"){
			steps  {
				sh "docker version"
				sh "mvn --version"
				echo "Build"
			}
		}
		stage ("Test"){
			steps {
				echo "Test"
			}
		}
		stage ("Integration Test"){
			steps  {
				echo "Integration Test"
			}
		}
	} 
	
	post {
		always {
			echo "Awsome I run always"
		}

		success {
			echo "I run when you are successful"

		}
		failure {
			echo "I run when you are failure"
		}
	}
}
