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
            	sh ''' 
            		export RELEASE_VERSION=$(cat gradle.properties | sed \'s/.*=//g\') && \
            		git tag -a "rel-$RELEASE_VERSION" -m "tagging with $RELEASE_VERSION" HEAD \
            		git push origin "rel-$RELEASE_VERSION"
            	'''
	            
	            withCredentials([
	            	usernamePassword(credentialsId: 'test-creds', usernameVariable: 'TEST_USERNAME1', passwordVariable: 'TEST_PASSWORD1')
	            ]) {
	            	sh './gradlew -Pnot.provided=$NOT_PROVIDED_VAR printenv'   
	            }
            }
        }
    }
}
