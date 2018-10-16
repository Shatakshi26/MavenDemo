#!/usr/bin/env groovy

pipeline
{
agent any
 
 tools { 
        maven 'Maven 3.5.4' 
        jdk 'jdk8' 
    }
stages{
	
stage('Build'){

	steps{
	checkout scm

	bat 'mvn clean install'

	}
    
 }
  
  stage('test'){
 
   steps{
    
    // Any maven phase that that triggers the test phase can be used here.
	 
   script{
     
   bat 'mvn test -B'
	
    if (currentBuild.result == 'UNSTABLE'){
  
  	currentBuild.result = 'FAILURE'
  
	throw err
	 
   }
 
 step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
	
    }
 
  }

   }
 
  stage('deploy'){

	   steps{
 
   echo "Im deploying now!"

	bat 'scp target/*.jar C:/Users/ShatakshiPandey/Downloads/apache-tomcat-9.0.12-windows-x64/apache-tomcat-9.0.12/webapps'

	   }
}
}
}
