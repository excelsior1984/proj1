pipeline {

agent any
environment {
      JAVA_HOME="${tool 'jdk8'}"
      PATH="${env.JAVA_HOME}/bin:${env.PATH}"
      CC = 'clang'
}


tools {
      jdk 'jdk8'
      maven 'maven3'
}

stages {
      stage('Install') {
           steps {
  	       sh 'java -version'
	       echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
	       echo "JAVA_HOME=  ${env.JAVA_HOME}  PATH=  ${env.PATH}""
//            	 sh "mvn clean test"
           }
	   post {
	   	always {
		       junit '**/target/*-reports/TEST-*.xml'
		}
           }
       }
}
}
