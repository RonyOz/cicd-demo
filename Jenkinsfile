pipeline {
	agent any

	options {
		timestamps()
	}

	stages {
		stage('Build') {
			steps {
				sh 'chmod +x mvnw && ./mvnw -B -ntp clean package -DskipTests'
			}
		}

		stage('Docker Build') {
			steps {
				sh 'docker build -t mi-app:latest .'
			}
		}

		stage('Test') {
			steps {
				sh "chmod +x mvnw && ./mvnw -B -ntp -DforkCount=0 -Dtest='!SeleniumExampleTest' test"
			}
		}

		stage('Integracion') {
			steps {
				echo 'Pipeline ejecutado desde SCM con Jenkinsfile versionado en el repositorio.'
			}
		}
	}

	post {
		always {
			junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
		}
	}
}
