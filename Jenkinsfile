pipeline {
  agent any
  tools { 
        maven 'Maven_3_8_4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=webappdevsecproject -Dsonar.organization=webappdevsecproject -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=$SONAR_TOKEN'
			}
    }
stage('RunSCAAnalysisUsingSnyk') {
  steps {
    withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
      sh 'mvn snyk:test'
    }
  }
}
	
