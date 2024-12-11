//This is scripted pipeline sample
node
{
  //   /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.9/bin

   def mavenHome=tool name:  "maven-3.9.9"
  stage('git checkout')
  {
  git branch: 'development', credentialsId: 'd8f5bb40-ee7a-41f2-a72d-0fcc8eb6b07b', url: 'https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git'
  }
  stage('Build')
  {
     sh "${mavenHome}/bin/mvn clean package"
  }
  stage('SQ Report')
  {  
     sh "${mavenHome}/bin/mvn clean sonar:sonar"   
  }

  stage('upload artifactt')
  {
    sh "${mavenHome}/bin/mvn clean deploy"
  }

  stage('DeployIntoTomcat')
  {
   sshagent(['12448eed-30eb-4f85-836d-1aae3fa0bee2']) 
   {

    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.201.194.103:/opt/apache-tomcat-9.0.97/webapps/"
    
   }
  }
	
}
