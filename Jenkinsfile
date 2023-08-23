pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=caseapp -Dsonar.organization=caseapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=bfd8c8e9d341686107d04bf4b336909f8c825217'
			}
    }
  
	// stage('RunSCAAnalysisUsingSnyk') {
  //           steps {		
	// 			withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
	// 				sh 'mvn snyk:test -fn'
	// 			}
	// 		}
  //   }	


//building docker image
// stage('Build') { 
//             steps { 
//                withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
//                  script{
//                  app =  docker.build("adegokeimage")
//                  }
//                }
//             }
//     }

	// stage('Push') {
  //           steps {
  //               script{
			
  //                   docker.withRegistry("https://585943330578.dkr.ecr.us-east-1.amazonaws.com", "ecr:us-east-1:aws-credentials") 
	// 		{
  //                   app.push("latest")
  //                   }
  //               }
  //           }
  //   	}


  }
}
