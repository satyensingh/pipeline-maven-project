pipeline {
	agent any
	
	tools {
		jdk 'localJDK'
		maven 'localMaven'
	}

	stages {
		stage ('Build'){
			steps {
				bat script: 'mvn clean package'
			}
			post {
				success {
					echo 'Archiving the Artifacts'
					archiveArtifacts '**/*.war'
				}
			}
		}
		stage ('Deploy to Staging'){
			steps {
				echo 'Deploying to staging server need manual approval'
				timeout(2) {
					input 'Approve Production Deployment?'
				}
				deploy adapters: [tomcat8(credentialsId: 'fc29fbea-a440-4146-8bf0-dd8e0e199d22', path: '', url: 'http://localhost:8989')], contextPath: null, war: '**/*.war'
			}
			post {
				success{
					echo 'Deployed!'
				}
				failure {
					echo 'Failed to deploy'
				}
			}
		}
	}
}
