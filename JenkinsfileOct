node
{
	properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
	def mavenHome=tool name: "maven-3.9.9"
	stage('checkout')
	{
		git branch: 'developement', credentialsId: '0d21a676-92f7-4609-8ce5-d1fa5387d808', url: 'https://github.com/AnilBabu1011/maven-web-app-project-kk-funda.git'
   }
   stage('build artifact')
   {
       sh "${mavenHome}/bin/mvn clean package"
   }
   stage('SQReport')
   {
		sh "${mavenHome}/bin/mvn clean sonar:sonar"
   }
   stage('deploy artifact into nexus')
   {
		sh "${mavenHome}/bin/mvn clean deploy"
   }
   stage('DeployintoTomcat')
   {
		sshagent(['f2e24f63-6283-44ed-8468-1fa73cb031d1']) 
		{
			sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.3.92:/opt/apache-tomcat-9.0.97/webapps"
		}
   }
}//node closed



