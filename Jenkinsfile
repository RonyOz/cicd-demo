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
				sh 'mvn -B package -DskipTests'
			}
		}

		stage('Docker Build') {
			steps {
				sh 'docker build -t mi-app:latest .'
			}
		}

		stage('Test') {
			steps {
				sh 'mvn -B test'
			}
		}

		stage('Integracion') {
			steps {
				echo 'Pipeline listo para ejecutarse como "Pipeline script from SCM" en Jenkins.'
			}
		}
	}
}
