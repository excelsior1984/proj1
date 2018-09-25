pipeline {
    agent {
    	  node {
    	       env.JAVA_HOME="${tool 'jdk8'}"
    	       env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
    	       sh 'java -version'
	  }
    }
    tools {
        jdk 'jdk8'
        maven 'maven3'
    }
    stages {
        stage('Install') {
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