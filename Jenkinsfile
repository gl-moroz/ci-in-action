pipeline {
    agent any
    stages {
        stage('Checkout') {
        	steps {
        		//checkout scm
        		checkout([$class: 'GitSCM', branches: [[name: '**']]])
        		sh 'git status'
        		sh 'git config user.name jenkins'
				sh 'git config user.email jenkins@example.com'
        	}
        }
        stage('Build') { 
            steps {
	            withCredentials([usernamePassword(credentialsId: 'test-creds', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
				    sh ''' 
	            		export RELEASE_VERSION=$(cat gradle.properties | sed \'s/.*=//g\') && \
	            		git tag -a \"rel-$RELEASE_VERSION\" -m \"tagging with $RELEASE_VERSION\" HEAD && \
	            		git push https://${GIT_USERNAME}:${GIT_PASSWORD}@https://github.com/gl-moroz/ci-in-action.git \"rel-$RELEASE_VERSION\"
            		'''
				}
	            
	            withCredentials([
	            	usernamePassword(credentialsId: 'test-creds', usernameVariable: 'TEST_USERNAME1', passwordVariable: 'TEST_PASSWORD1')
	            ]) {
	            	sh './gradlew -Pnot.provided=$NOT_PROVIDED_VAR printenv'   
	            }
            }
        }
    }
}
