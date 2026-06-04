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
				pipeline {
				  agent {
				    docker {
				      image 'maven:3.8.8-openjdk-11'
				      args '-u root:root'
				    }
				  }

				  stages {
				    stage('Test') {
				      steps { 
				        checkout scm
				        sh 'mvn clean test'
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
				    always { cleanWs() }
				  }
				}

