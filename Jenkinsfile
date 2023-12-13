pipeline {
    agent {
		docker {
			image 'node'
		    args '-u root:root'

		}
	}


	
    stages {
        stage('pre-build') {
            steps {
                script {
					sh 'apt-get update'
					sh 'apt-get install default-jre'
					
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
								withSonarQubeEnv('sonar-server-env') {
								 sh "npx sonarqube-scanner "
						}

						sh 'sleep 80000'

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
