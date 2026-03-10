pipeline {
  agent any
  tools { 
        maven 'Maven_3_8_4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=webappdevsecproject -Dsonar.organization=webappdevsecproject -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=882790e09f5d05630d2580489ed1729e36160486'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test'
				}
			}
    }		
  }
}
