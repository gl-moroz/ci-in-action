pipeline {
    agent any 
    stages {
        stage('Checkout') {
        	steps {
        		checkout scm
        		sh 'git status'
        	}
        }
        stage('Build') { 
            steps {
            	sh 'git branch --set-upstream $BRANCH_NAME origin/$BRANCH_NAME'
            
            	withCredentials([
            		usernamePassword(credentialsId: 'test-creds', usernameVariable: 'TEST_USERNAME1', passwordVariable: 'TEST_PASSWORD1')
            	]) {
            		sh './gradlew -Pnot.provided=$NOT_PROVIDED_VAR printenv'   
            	}
            }
        }
    }
}