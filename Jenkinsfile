pipeline {  
	agent any
	parameters {
        	string(name: 'Environment', defaultValue: 'Sandbox', description: 'Environment Name')
		string(name: 'Workers', defaultValue: '1', description: 'Number of Workers for the Application')
		string(name: 'Workers_Type', defaultValue: 'MICRO', description: 'Worker Type')
		string(name: 'Application_Name', defaultValue: 'ChangeIt', description: 'Application Name')
		string(name: 'Mule_Version', defaultValue: '4.3.0', description: 'Runtime Version')
	}
	options {
		timeout(time: 1, unit: 'HOURS') 
	}
	
	stages {
		stage('Build Application') {
	        	steps {
				echo 'Build Appplication...' 
	                	bat 'mvn clean install'
			}
		}
	        stage('Test') {
	               steps {
	                  	echo 'Test Appplication...' 
        		  	bat 'mvn clean test'      
        		}   
		}
               stage('Deploy CloudHub') {
		       environment {
                		ANYPOINT_CREDENTIALS = credentials('Anypoint_Studio')
            		}
		       steps {
			       echo 'Deploying only because of code commit...'
			       bat "mvn package deploy -DmuleDeploy"
		       }    
	       }  
	}
}
