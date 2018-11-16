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
            		def v00 = v[0][0]
            		def v01 = v[0][1]
            		def v02 = v[0][2]
            		def v10 = v[1][0]
            		def v11 = v[1][1]
					
					sh "echo Processing ${v00}"            	    
					sh "echo Processing ${v01}"
					sh "echo Processing ${v02}"
					sh "echo Processing ${v10}"
					sh "echo Processing ${v11}"
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
  def matcher = readFile('gradle.properties') =~ 'set\\.version[\\s]*=[\\s]*(.+)[\\s]*$'
  //matcher ? matcher[0][1] : null
  matcher ?: null
}
