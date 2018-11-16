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
            	script {
            		def matcher = readFile('gradle.properties') =~ 'set.version=(.+)'
  					def v = matcher ? matcher[0][1] : null
					//env.release_ver =  sh (script: 'cat gradle.properties | sed \'s/.*=//g\'', returnStdout: true).trim()
					sh 'echo Processing ${v}'            	    
            	}

	            
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
