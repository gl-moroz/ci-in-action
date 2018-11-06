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
            	withCredentials([
            		usernamePassword(credentialsId: 'test-creds', usernameVariable: 'TEST_USERNAME1', passwordVariable: 'TEST_PASSWORD1')
            	]) {
            		sh './gradlew -Pnot.provided=$NOT_PROVIDED_VAR printenv'   
            	}
            }
        }
    }
}