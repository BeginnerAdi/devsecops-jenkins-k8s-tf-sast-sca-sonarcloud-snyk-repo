pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=evsecops-buggywebapp-ag -Dsonar.organization=evsecops-buggywebapp-ag -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=16ac913a15c90ce507be1bf2f0525f72207e1d8d'
			}
        } 
	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
