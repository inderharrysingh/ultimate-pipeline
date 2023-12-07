pipeline {
    agent {
		docker {
			label 'node:lts-buster-slim'
		}
	}
	

	
    stages {
        stage('testing') {
            steps {
                script {
					sh 'echo "Starting the testing step...."'
					sh 'echo $TAG'
                }
            }
}
	        
        stage('build') {
            	steps {
                	sh 'npm cache clean --force'
                	sh 'npm ci'
	
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
