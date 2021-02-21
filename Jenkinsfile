
//Declarative [ declarative pipeline is we would not need to have a node anymore. So, we can directly
//say pipeline and over here in the pipeline you can configure a agent.]


pipeline {
	// agent any
	agent { docker { image 'maven:3.6.3'} }
	stages {
		stage('Build') {
			steps {
				echo "mvn --version"
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
			echo "I run always"
		}
		success {
			echo "I run when you are successful"
		}
		failure {
			echo "I run when you are fail"
		}
	}
}
	