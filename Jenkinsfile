node('flipkart-node')
             
    		   {

		    def mavenHome = tool name: "maven3.6.2"    
  		    stage("CheckOutCode")
                      {
                         git branch: 'development', credentialsId: 'fded1d48-0bf8-4455-9ea2-738d357acb89', url: 'https://github.com/suneetha1155/maven-web-application.git'
		      }
                   stage("Build")
		      {
			sh "${mavenHome}/bin/mvn clean package"     
		      }
		   stage("ExecuteSonarQubeReport")
		      {
		        sh "${mavenHome}/bin/mvn sonar:sonar"
 	               }
		    stage("UploadArtifactsintoNexus")
		      {
		        sh "${mavenHome}/bin/mvn deploy"
 	               }
stage("DeployAppTomcat")
               {
                 sshagent(['6068c50d-4823-4167-8d30-3a25f6004064'])         
		  {
		  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.108.41.58:/opt/apache-tomcat-9.0.56/webapps/"
		   }
		   }
		   stage('EmailNotification')

{
emailext body: '''Build Over.


Regards
Suneetha''', subject: 'Build Over.', to: 'suneetha1155@gmail.com'
}
	            }
