pipeline {  
	agent any
	parameters {
        	string(name: 'Environment', defaultValue: 'Sandbox', description: 'Environment Name')
		string(name: 'Workers', defaultValue: '1', description: 'Number of Workers for the Application')
		string(name: 'Workers_Type', defaultValue: 'MICRO', description: 'Worker Type')
		string(name: 'Application_Name', defaultValue: 'ChangeIt', description: 'Application Name')
		string(name: 'Mule_Version', defaultValue: '4.3.0', description: 'Runtime Version')
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
			       bat "mvn package deploy -DmuleDeploy -Danypoint.environment=${params.Environment} -Danypoint.username=$ANYPOINT_CREDENTIALS_USR -Danypoint.password=$ANYPOINT_CREDENTIALS_PSW -Danypoint.workers=${params.Workers} -Danypoint.workersType=${params.Workers_Type} -Danypoint.applicationName=${params.Application_Name} -Danypoint.muleVersion=${params.Mule_Version} -DobjectStoreV2=true"
		       }    
	       }  
	}
}
