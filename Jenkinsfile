pipeline {

node('aaa') {
   	 env.JAVA_HOME="${tool 'jdk8'}"
   	 env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
  	 sh 'java -version'
}
    agent any


    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

    stages {
        stage('Install') {
	label 'aaa'
            steps {
            	 sh "mvn clean test"
            }
            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                }
            }
        }
    }
}
