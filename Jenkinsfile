pipeline {
    agent any

//	tools {
//		maven 'maven3.6'
//	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
	
		stage('Build') {
			steps {
				sh 'mvn install -Dmaven.test.skip=true'
			}
		}
		
		stage('Unit Tests') {
			steps {
				sh 'mvn compiler:testCompile'
				sh 'mvn surefire:test'
				junit 'target/**/*.xml'
			}
		}

	
		stage('Deployment') {
			steps {
				sh 'sshpass -p "madhu" scp target/gamutgurus.war madhu@172.17.0.4:/home/madhu/Distros/apache-tomcat-8.5.64/webapps'
				sh 'sshpass -p "madhu" ssh madhu@172.17.0.4 "/home/madhu/Distros/apache-tomcat-8.5.64/bin/startup.sh"'
	    	}
		}
    }
}
