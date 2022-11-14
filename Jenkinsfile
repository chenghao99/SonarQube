pipeline {
	agent any
	stages {
		stage ('Checkout') {
			steps {
				git branch:'main', url: 'https://github.com/ict3x03-Learn4Fund/Learn4Fund'
			}
		}
		stage('Code Quality Check via SonarQube') {
			steps {
				script {
					def scannerHome = tool 'SonarQube';
						withSonarQubeEnv('SonarQube') {
						sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://172.18.0.3:9000 -Dsonar.login=sqp_e6a0a6ec85cf65eece6aac57e7bd0af82a335518"
						}
				}
			}
		}
	}
	post {
		always {
			recordIssues enabledForFailure: true, tool: sonarQube()
		}
	}
}