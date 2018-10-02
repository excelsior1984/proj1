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

        stage ('deploy'){

            steps{

                configFileProvider([configFile(fileId: '49a1c083-fc08-4126-99e8-c25b786e72c6', variable: 'SETTINGS')]) {

                    sh "mvn -s $SETTINGS deploy -DskipTests -Dartifactory_url=${env.ARTIFACTORY_URL}"

                }

            }

        }

}
}
