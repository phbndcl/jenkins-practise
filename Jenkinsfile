pipeline {
    agent any
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin;$PATH"
	}
    stages {
        stage('Build') {
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
			stage('Test') {
            steps {
                echo "Test"
            }
        }
		stage('Intergration Test') {
            steps {
                echo "Integration Test"
            }
        }
    }
}