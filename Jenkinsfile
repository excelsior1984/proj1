pipeline {


	 agent any


    tools {
        jdk 'jdk8'
        maven 'maven3'
    }

    stages {
        stage('Install') {

            steps {
	       	 env.JAVA_HOME="${tool 'jdk8'}"
   	 env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
  	 sh 'java -version'

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
