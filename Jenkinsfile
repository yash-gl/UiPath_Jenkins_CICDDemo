pipeline {
	    agent any
	

	        // Environment Variables
	        environment {
	        	MAJOR = '1'
	        	MINOR = '1'

				//UIPATH_ORCH_CREDENTIALS = UserPass('ui_orch_dev_jenkins')
	        	//Orchestrator Services
	        	UIPATH_ORCH_URL = "https://gl-ui-orchestrator.canadaeast.cloudapp.azure.com"
	        	//UIPATH_ORCH_LOGICAL_NAME = "anupaminc"
	        	UIPATH_ORCH_TENANT_NAME = "Development"
	        	UIPATH_ORCH_FOLDER_NAME = "yash.brahmbhatt@ad's workspace"
			}
	

	     	stages {
	

	        // Printing Basic Information
	        	stage('Preparing'){
	            	steps {
	                	echo "Jenkins Home ${env.JENKINS_HOME}"
	                	echo "Jenkins URL ${env.JENKINS_URL}"
	                	echo "Jenkins JOB Number ${env.BUILD_NUMBER}"
	                	echo "Jenkins JOB Name ${env.JOB_NAME}"
	                	echo "GitHub Branch Name ${env.BRANCH_NAME}"
	                	checkout scm
	            	}
	        	}
	

	         	// Build Stages
	        	stage('Build') {
		            steps {
		                echo "Building..with ${WORKSPACE}"
						UiPathPack(
							credentials: UserPass('ui_orch_dev_jenkins'), 
							orchestratorAddress: '${UIPATH_ORCH_URL}', 
							orchestratorTenant: '${UIPATH_ORCH_TENANT_NAME}', 
							outputPath: '${WORKSPACE}\\Output', 
							projectJsonPath: '${WORKSPACE}', 
							useOrchestrator: true, 
							version: AutoVersion()
						)
					}
	        	}
		         // Test Stages
		        stage('Test') {
	    	        steps {
	        	        echo 'Testing..the workflow...'
		            }
		        }
	

	    	     // Deploy Stages
	        	stage('Deploy to UAT') {
	            	steps {
	                	echo "Deploying ${BRANCH_NAME} to UAT "
	            	}
	        	}


	

		         // Deploy to Production Step
	    	    stage('Deploy to Production') {
	        	    steps {
	            	    echo 'Deploy to Production'
	            	}
	        	}
	    	}

		    // Options
		    options {
	    	    // Timeout for pipeline
	        	timeout(time:80, unit:'MINUTES')
	        	skipDefaultCheckout()
	    	}


	

	    // 
	    	post {
		        success {
		            echo 'Deployment has been completed!'
	    	    }
	        	failure {
	          		echo "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.JOB_DISPLAY_URL})"
	        	}
	        	always {
		            /* Clean workspace if success */
	            	cleanWs()
	        	}
	    	}
	

	}
