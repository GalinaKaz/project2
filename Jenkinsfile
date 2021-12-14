pipeline {
    agent any

    stages {
        stage('Testing All...') {
            when {
                expression{
                    LANG=='All'
                }
            }
            steps {
                echo 'running all....'
            }
        }

        stage('Testing C') {
	        when {
	            expression{
		            LANG=='C'
	            }
            }
            steps {
                echo 'running C....'
                sh '''
                cd ${HOME}/scripts
                ./C_prog
                '''
            }
        }

        stage('Testing Python') {
	        when {
	            expression{
		            LANG=='Python'
	            }
            }
            steps {
                echo 'running Python....'
            }
        }

        stage('Testing Bash') {
	        when {
	            expression{
		            LANG=='Bash'
	            }
            }
            steps {
                echo 'running Bash....'
            }
        }
         
   }


   post {   
		always {
			echo "this is the LANG: $LANG"
		}   
		success {   
			sh 'echo "BUILD_NUMBER=$BUILD_NUMBER success" >> report' 
		}   
		failure {
			sh 'echo "BUILD_NUMBER=$BUILD_NUMBER failed" >> report'   
		}   
		unstable {   
			echo 'I will only get executed if this is unstable'   
		}   
   }
}
