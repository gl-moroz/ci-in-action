pipeline {
    agent any 
    stages {
        stage('Checkout') {
        	steps {
        		//checkout scm
        		checkout([$class: 'GitSCM', branches: [[name: '**']]])
        		sh 'git status'
        	}
        }
        stage('Build') { 
            steps {
            	sh 'export RELEASE_VERSION=$(cat gradle.properties | sed \'s/.*=//g\')'
            	sh 'echo Processing $RELEASE_VERSION'
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