node('master') {

stage ('checkout code'){
	checkout scm
}
	
stage ('Build'){
	sh "mvn clean install"
}
stage ('Build Docker Image'){
	sh "docker build -t tuhi19/mavenbuild:0.0.1 ."
}
stage('Push to Docker Hub'){
	sh "docker push tuhi19/mavenbuild:0.0.1"
}
stage('Remove Previous Container'){
	 try{
		sh "docker rm -f mavenbuild"
	}
	catch(error){
		//  do nothing if there is an exception
	}	
}		
stage('Deploy to Stage Environment'){
	sh "docker run -d -p 8083:8080 mavenbuild:0.0.1"
}
}
