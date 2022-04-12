//Declarative [ declarative pipeline is we would not need to have a node anymore. So, we can directly
//say pipeline and over here in the pipeline you can configure a agent.]


pipeline {
	
	agent { docker { image 'maven:3.6.3' } }
// 	environment {
// 		dockerHome = tool 'myDocker'
// 		mavenHome = tool 'myMaven'
// 		PATH= "$dockerHome/bin:$mavenHome/bin:$PATH" 
// 	}
	stages {
		stage('Build') {
			steps {
				sh "mvn --version"
				sh " docker --version"
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
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
			echo "Test run completed"
		}
		success {
			echo "Successfully!"
		}
		failure {
			echo "Failed!"
		}
		 changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
	}
}
