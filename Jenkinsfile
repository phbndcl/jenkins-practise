pipeline {
    agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
    stages {
        stage('Checkout') {
            steps {
				sh "mvn --version"
				sh "docker --version"
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_URL - $env.BUILD_URL"
				echo "BUILD_TAG - $env.BUILD_TAG"
				}
        	}
			stage('Compile'){
				steps {
					sh "mvn clean compile"
				}
			}
			stage('Test') {
            steps {
                sh "mvn test"
            }
        }
		stage('Intergration Test') {
            steps {
                sh "mvn failsafe:integration-test failsafe:verify"
            }
        }
		stage('Package') {
			steps {
				sh "mvn package -DskipTest"
			}
		}
		stage('Build Docker Image') {
			steps {
				script {
					dockerImage = docker.build("phb95/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry( '', 'dockerhub' ) {
						dockerImage.push();
						dockerImage.push('latest')
					}
				}
			}
		}
    }
}