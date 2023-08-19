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
		    
			sh 'docker build -t amiyaranjansahoo/image1:v1'
			}
			
		}
		
		stage('Login to Docker hub and upload'){
			steps{
		    
			withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerpassword')]) {
			sh 'docker login -u amiyaranjansahoo -p ${dockerpassword}'
			}
		}
			
		}
	}
}
