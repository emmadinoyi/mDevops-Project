pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=closeapp -Dsonar.organization=closeapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=bda611e17f0f9e10668d08ffcad247b3a9b101f5'
			}
    }
  
	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }	


//building docker image
stage('Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                 script{
                 app =  docker.build("emmaimage")
                 }
               }
            }
    }

	stage('Push') {
            steps {
                script{
			
                    docker.withRegistry("https://514382470131.dkr.ecr.us-east-1.amazonaws.com", "ecr:us-east-1:aws-credentials") 
			{
                    app.push("latest")
                    }
                }
            }
    	}



  stage('Kubernetes deployment app'){
    steps {

      withKubeConfig([credentialsId: 'kubelogin']){
        sh('kubectl delete all --all -n devsecops')
        sh('kubectl apply -f deployment.yaml --namespace=devsecops')
      }
    }
  }


  }
}
