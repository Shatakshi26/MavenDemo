#!/usr/bin/env groovy
pipeline{
 agent { label 'java8' }
 stages{
	stage('Build'){
	node{
	checkout scm
	sh 'mvn clean install'
	}
     }
    stage('test'){
    node{

    try {
        // Any maven phase that that triggers the test phase can be used here.
        sh 'mvn test -B'
    } catch(err) {
        if (currentBuild.result == 'UNSTABLE')
    	currentBuild.result = 'FAILURE'
  	throw err
    }finally{
  step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
}
   }
   stage('deploy'){
    echo "Im deploying now!"
	   when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS'
              }
            }
}
}
}