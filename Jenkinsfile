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
            		def v = version()
            		def v2 = version2()
					
					sh "echo Processing ${v} | ${v2}"            	    
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

@NonCPS
def version() {
  def matcher = readFile('gradle.properties') =~ 'set.version=(.+)'
  matcher ? matcher[0][1] : null
}

@NonCPS
def version2() {
  def matcher = readFile('gradle.properties') =~ 'set.version=(.+)'
  matcher ? matcher[0][2] : null
}
