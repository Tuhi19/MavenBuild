node('master') {

stage ('checkout code'){
	checkout scm
}
	
stage ('Build'){
	sh "cd mavenbuild"
	sh "mvn clean install"
	sh "sudo docker build -t mavenbuild ."
	sh "sudo docker push mavenbuild"
}

stage ('Test Cases Execution'){
	sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
}

stage ('Sonar Analysis'){
	//sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:80'
}

stage ('Archive Artifacts'){
	archiveArtifacts artifacts: 'target/*.war'
}
	
stage ('Deployment'){
	sh 'cp target/*.war /opt/tomcat8/webapps'
}
}
