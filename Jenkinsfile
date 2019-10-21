node{
 stage('Git Checkout'){
	git branch: 'dockercicd', url: 'https://github.com/mahato861/devopsprojects.git'  
 }
 stage('Maven Package'){
	def mvnHome = tool name: 'maven-3', type: 'maven'
	sh "${mvnHome}/bin/mvn clean package"
 	sh 'mv target/myweb*.war target/myweb.war'
 }
 
 stage('Build Docker Imager'){
   sh 'docker build -t mahato861/myweb:0.0.1 .'
 }
 stage('Push to Docker Hub'){
	 withCredentials([string(credentialsId: 'dockerHubPwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u mahato861 -p ${dockerHubPwd}"
     }
	 sh 'docker push mahato861/myweb:0.0.1'
 }
 stage('Remove Previous Container'){
	try{
		def dockerRm = 'docker rm -f myweb'
		sshagent(['docker-dev']) {
			sh "ssh -o StrictHostKeyChecking=no ubuntu@3.92.208.69 ${dockerRm}"
		}
	}catch(error){
		//  do nothing if there is an exception
	}
 }

stage('Remove Previous Image'){
	try{
		def dockerRmi = 'docker rmi mahato861/myweb'
		sshagent(['docker-dev']) {
			sh "ssh -o StrictHostKeyChecking=no ubuntu@3.92.208.69 ${dockerRmi}"
		}
	}catch(error){
		//  do nothing if there is an exception
	}
 }
 stage('Deploy to Dev Environment'){
   def dockerRun = 'docker run -d -p 8080:8080 --name myweb mahato861/myweb:0.0.1 '
   sshagent(['docker-dev']) {
    sh "ssh -o StrictHostKeyChecking=no ubuntu@3.92.208.69 ${dockerRun}"
   }

 }
 
}
