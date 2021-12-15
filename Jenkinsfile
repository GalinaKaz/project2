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
                cd ${WORKSPACE}/scripts
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
                cd ${WORKSPACE}/scripts
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
                cd ${WORKSPACE}/scripts
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
                cd ${WORKSPACE}/scripts
                bash Bash_prog
                '''
            }
        }

        stage('Reporting Results') {
         steps {
            echo 'Reporting Results process to /var/jenkins_home/Log/report file '
            sh '''
	        report_file="${WORKSPACE}/Logs/report"
            mkdir -p ${WORKSPACE}/Logs
              if [ -f "${report_file}" ]; then
                echo "file ${report_file} exists"
              else
	              touch ${report_file}
              fi
	        date >> ${report_file}
	        echo "JOB_NAME=$JOB_NAME" >> ${report_file}
            echo "Build Number $BUILD_NUMBER" >> ${report_file}
            echo "The script runs with parameter LANG=${LANG}" >> ${report_file}
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
