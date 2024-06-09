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
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=retail-store-jenkins-project -Dsonar.organization=cehv9solutions -Dsonar.host.url=http://172.17.0.4:9000 -Dsonar.token=squ_30c59cf2c28d3459e1769413baf58293054c0103'
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
