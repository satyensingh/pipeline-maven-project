pipeline {
	agent any

	stages {
		stage ('Build'){
			steps {
				bat script: 'mvn clean package'
			}
		}
	}
}
