pipeline{
	agent any
	
	stages{
		/*
		stage('git clone'){
			steps{
				git credentialsId: 'git', url: 'https://github.com/amiyaranjansahoo/docker-cicd-jh.git'
			}
		}
		*/
		stage('maven build'){
		    tools {
             maven 'mvn3'
            }
			steps{
				sh 'mvn clean package'
			}
		}
		
		stage('Build the docker image'){
			steps{
		    
			sh 'docker build . -t amiyaranjansahoo/image1:v1'
			}
			
		}
		
		stage('Login to Docker hub and upload'){
			steps{
		    
			withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerpassword')]) {
			sh 'docker login -u amiyaranjansahoo -p ${dockerpassword}'
			sh 'docker push amiyaranjansahoo/image1:v1'
			}
		}
			
		}
		
		stage('Transfer to remote server'){
		    
			steps{
				sshagent(['tomcat']) {
	sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.47.189 docker container rm -f myweb' 
    sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.47.189 docker run -itd -p 8080:8080 --name myweb amiyaranjansahoo/image1:v1 '
}
				
			}
		}
	}
}
