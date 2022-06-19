//Declarative
pipeline {
	agent any
	//agent { docker { image 'maven:3.6.3'}}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage ("Checkout"){
			steps  {
				sh "docker version"
				sh "mvn --version"
				echo "Build"
				echo "PATH - $PATH"
			}
		}
		stage ("Compile"){
			steps {
				sh "mvn clean compile"
			}
		}

		stage (Test) {
			steps {
				sh "mvn test"
			}
		}

		stage ("Integration Test"){
			steps  {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage ("Package"){
			steps  {
				sh "mvn package -DskipTests"
			}
		}

		stage ("build docker image") {
			steps {
				script{
					dockerImage = docker.build("mohammedoufi/currency-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage ("push docker image") {
			steps {
				script{
					docker.withRegistry('','c2117250-625a-42c9-b88c-159b6836b6aa'){
						dockerImage.push();
						dockerImage.push('latest');
					}
					
				}
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
