pipeline {
    agent {
		docker {
			image 'node'
		    args '-u root:root'

		}
	}

	environment {

                scannerHome = tool 'SonarScanner'

  }
	

	
    stages {
        stage('pre-build') {
            steps {
                script {
					sh ' echo "nothing..."'
                }
            }
}
	        
        stage('build') {
            	steps {
                	sh 'npm install'	
    	   	 }
	        }

		  stage('SonarQube Analysis') {
				
				steps {
					
					script {	
						  		echo "${scannerHome}"
								sh 'sleep 80000'					
								withSonarQubeEnv('sonar-server-env') {
								 sh "${scannerHome}/bin/sonar-scanner"
						}

					}
			  }
		}

		
			stage("Quality gate") {
				steps {
					waitForQualityGate abortPipeline: true
				}
			}
	

	// stage('docker push'){
	// 	steps{
	//   	  script {
	// 		withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
    //                     	sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"	
	// 						sh "docker build -t $IMAGE:v$TAG ."
	// 						sh "docker push $IMAGE:v$TAG"
							
    //                 }
	// 		}
    //      }
    //  }
	


	// stage('update gitrepo for argo cd '){
	// 	steps{
	// 		 script {

	// 				cleanWs()
    //                 withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
    //                     sh """
    //                     git clone https://inderharrysingh:${GITHUB_TOKEN}@github.com/inderharrysingh/devSecOps-image.git
    //                     cd devSecOps-image
	// 					chmod +x update-tag
	// 					./update-tag $TAG
    //                     git commit -am "Commit message"
    //                     git push
    //                     """
    //                 }
    //             }
	// 	}
	// }

}
}
