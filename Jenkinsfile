
//Declarative [ declarative pipeline is we would not need to have a node anymore. So, we can directly
//say pipeline and over here in the pipeline you can configure a agent.]


node('jenkins-slave') { 

	stages {
		stage('Checkout') {
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
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker image'){
			steps {
				//"docker build -t passdocker/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage=docker.build("passdocker/currency-exchange-devops:${env.BUILD_TAG}")
				}
 			}
		}
		stage('Push Docker image'){
			steps {
				script {
					docker.withRegistry(' ', '93fef224-3018-4463-a893-0c5f3d57b041'){
						dockerImage.push();
					    dockerImage.push('latest');
					}
					
				}
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
	
