pipeline {
    agent any

    tools { 
        maven 'Maven_3_8_4'
    }

    stages {

        stage('Compile and Run Sonar Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh '''
                    mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=webappdevsecproject \
                    -Dsonar.organization=webappdevsecproject \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }

        stage('Run SCA Analysis Using Snyk') {
            steps {
                withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                    sh 'mvn snyk:test'
                }
            }
        }

    }
}
	
