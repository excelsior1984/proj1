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

       
       stage('deploy') {
           steps{
		 configFileProvider(
		         [configFile(fileId: 'settings.xml')]) {
			 	sh 'mvn clean package'
	//                    sh "mvn -s $SETTINGS deploy -DskipTests -Dartifactory_url=${env.ARTIFACTORY_URL}"
    			 }
          }
      }
}
}
