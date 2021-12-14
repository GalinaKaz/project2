pipeline {
    agent any

    stages {
        stage('Build: C,Python,Bash') {
            when {
                expression{
                    LANG=='All'
                }
            }
            steps {
                echo 'All scripts are running....'
                sh '''
                cd ${HOME}/scripts
                ./C_prog
                python3 Py_prog.py
                bash Bash_prog
                '''
            }
        }

        stage('Build: C') {
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

        stage('Build: Python') {
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

        stage('Build: Bash') {
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

        stage('Reporting Results') {
         steps {
            echo 'Reporting Results process to /var/jenkins_home/Log/report file '
            sh '''
	        report_file="${HOME}/Logs/report"
            mkdir -p ${HOME}/Logs
              if [ -f "${report_file}" ]; then
                echo "file ${report_file} exists"
              else
	              touch ${report_file}
              fi
	        date >> ${report_file}
	        echo "USER=$USER JOB_NAME=$JOB_NAME" >> ${report_file}
            echo "Build Number $BUILD_NUMBER" >> ${report_file}
            echo "The script runs for parameter LANG=${LANG}" >> ${report_file}
	        echo "#############################" >> ${report_file}
            '''
         }
      }
         
   }


   post {   
		always {
			echo 'Post line - always runs'
		}   
		success {   
			echo 'Post line - runs after success'
		}   
		failure {
			echo 'Post line - runs after failure'
		}   
		unstable {   
			echo 'executed if run is unstable'
		}   
   }
}
