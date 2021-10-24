node 
 {
    def mavenhome = tool name: "maven3.8.3"
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])	       
  stage('checkOutCode'){
    git branch: 'development', credentialsId: '82c19a04-7f31-4602-8430-777975b23fd6', url: 'https://github.com/pendemestate/maven-web-application.git'
    }
  stage('Build'){
    sh "${mavenhome}/bin/mvn clean package"
    }

  stage('Build'){
    sh "${mavenhome}/bin/mvn clean sonar:sonar"
    }  
 
  stage('ExecuteSonarQubeReport'){
    sh "${mavenhome}/bin/mvn clean sonar:sonar"
    }  
	
  stage('UploadArtifactIntoNexusRepo'){
    sh "${mavenhome}/bin/mvn clean deploy"
    } 
	
  stage('DeployApplicationtoTomcat'){
    sshagent(['3b1ca054-7138-4d82-99dc-c89a95e91ac3']) {
	
	sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.109.37.92:/opt/apache-tomcat-9.0.54/webapps" 
      }
	
	}
	
  }
