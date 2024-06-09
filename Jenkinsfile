pipeline {
  agent {
  label {
    label 'cloudscan'
    retries 4
  }
}

  tools { 
        maven 'Maven3'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=retail-store-jenkins-project -Dsonar.organization=cehv9solutions -Dsonar.host.url=http://172.17.0.4:9000 -Dsonar.token=sqp_8ce3ff6c16aefdcee67d32894a459ec0dcad7950'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'snyk-api-token', variable: 'snyk-api-token')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
