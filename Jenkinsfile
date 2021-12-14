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
                sh '''
                cd ${HOME}/scripts
                ./C_prog
                python3 Py_prog.py
                bash Bash_prog
                '''
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
                sh '''
                cd ${HOME}/scripts
                python3 Py_prog.py
                '''
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
                sh '''
                cd ${HOME}/scripts
                bash Bash_prog
                '''
            }
        }
         
   }


   post {   
		always {
			echo "this is the LANG: $LANG ; pwd "
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
