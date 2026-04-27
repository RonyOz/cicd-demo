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
				sh 'chmod +x mvnw && ./mvnw -B package -DskipTests'
			}
		}

		stage('Docker Build') {
			steps {
				script {
					if (sh(script: 'command -v docker >/dev/null 2>&1', returnStatus: true) == 0) {
						sh 'docker build -t mi-app:latest .'
					} else {
						echo 'Docker no esta disponible en este agente; se omite Docker Build.'
					}
				}
			}
		}

		stage('Test') {
			steps {
				sh './mvnw -B test'
			}
		}

		stage('Integracion') {
			steps {
				echo 'Pipeline listo para ejecutarse como "Pipeline script from SCM" en Jenkins.'
			}
		}
	}
}
