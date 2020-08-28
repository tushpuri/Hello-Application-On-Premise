pipeline {  
	agent any
	parameters {
		string(name: 'Mule_Home', defaultValue: 'C:\AnypointStudio-7.5.1-win64\AnypointStudio\mule-enterprise-standalone-4.3.0', description: 'On-Premise location to deploy the application')
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
		       //environment {
                	//	ANYPOINT_CREDENTIALS = credentials('Anypoint_Studio')
            		//}
		       steps {
			       echo 'Deploying only because of code commit...'
			       bat "mvn package deploy -DmuleDeploy -Dmule.version=${params.Mule_Version} -Dmule.home=${params.Mule_Home} -DapplicationName=${params.Application_Name}"
		       }    
	       }  
	}
}
