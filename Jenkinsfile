pipeline{
	agent any
	
	stages{
		stage('git clone'){
			steps{
				git credentialsId: 'git', url: 'https://github.com/amiyaranjansahoo/docker-cicd-jh.git'
			}
		}
		
		stage('maven build'){
		    tools {
             maven 'mvn3'
            }
			steps{
				sh 'mvn clean package'
			}
		}
		
		stage('Deploy to tomcat'){
		    
			steps{
				sshagent(['tomcat']) {
					// some block
					sh 'mv target/*.war target/myweb.war'
					sh 'scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@172.31.47.189:/home/ec2-user/tomcat/webapps'
					sh 'ec2-user@172.31.47.189 /home/ec2-user/tomcat/bin/shutdown.sh'
					sh 'ec2-user@172.31.47.189 /home/ec2-user/tomcat/bin/startup.sh'
					
				}
			}
		}
	}
}
