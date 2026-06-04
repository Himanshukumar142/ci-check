pipeline {
	agent none

	stages {
		stage('Build & Test') {
			agent {
				docker {
					image 'maven:3.8.8-openjdk-11'
					args '-u root:root'
				}
			}

			steps {
				checkout scm
				sh 'mvn clean test'
			}
			steps {
				sh "mvn clean package"
			}
			steps{
				sh "docker build -t my-app ."
			}
			
			post {
				always {
					junit 'target/surefire-reports/*.xml'
					archiveArtifacts artifacts: 'target/surefire-reports/**', fingerprint: true
				}
			}
		}
	}

	post {
		always {
			cleanWs()
		}
	}
}

