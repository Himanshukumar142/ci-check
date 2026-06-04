pipeline {
	agent any

	stages {

		stage('Checkout') {
			steps {
				checkout scm
			}
		}

		stage('Build') {
			steps {
				sh 'mvn -B -DskipTests clean package'
			}
		}

		stage('Docker Build') {
			steps {
				sh 'docker build -t my-app:latest .'
			}
		}

		stage('Run') {
			steps {
				echo 'running the container'
				sh '''
					docker stop my-app || true
					docker rm my-app || true
					docker run -d --name my-app my-app:latest
				'''
			}
		}
	}
}

