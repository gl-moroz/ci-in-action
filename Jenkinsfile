pipeline {
    agent any
    parameters {
        string(name: 'release_ver')
    } 
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
            	script {
					env.release_ver =  sh (script: 'cat gradle.properties | sed \'s/.*=//g\'', returnStdout: true).trim()            	    
            	}

	            sh 'echo Processing ${env.release_ver}'
	            //sh 'git branch --set-upstream $BRANCH_NAME origin/$BRANCH_NAME'
	            
	            withCredentials([
	            	usernamePassword(credentialsId: 'test-creds', usernameVariable: 'TEST_USERNAME1', passwordVariable: 'TEST_PASSWORD1')
	            ]) {
	            	sh './gradlew -Pnot.provided=$NOT_PROVIDED_VAR printenv'   
	            }
            }
        }
    }
}
