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
      stage('install and sonar parallel') {
           steps {
	   parallel(install: {
  	          sh 'java -version'
	          echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
	          echo "JAVA_HOME=  ${env.JAVA_HOME}  PATH=  ${env.PATH}"
	          sh "mvn -U clean test cobertura:cobertura -Dcobertura.report.format=xml"
	       }, sonar: {
                   sh "mvn sonar:sonar -Dsonar.host.url=${env.SONARQUBE_HOST}"
	       })
	       
           }
	   post {
	   	always {
		       junit '**/target/*-reports/TEST-*.xml'
                       step([$class: 'CoberturaPublisher', coberturaReportFile: 'target/site/cobertura/coverage.xml'])
		}
           }
       }
       stage('deploy') {
           steps{
		 configFileProvider(
		         [configFile(fileId: 'maven-settings', variable: 'MAVEN_SETTINGS')]) {
			 	sh 'mvn -s $MAVEN_SETTINGS clean package'
	//                    sh "mvn -s $SETTINGS deploy -DskipTests -Dartifactory_url=${env.ARTIFACTORY_URL}"
    			 }
          }
      }
}
}
