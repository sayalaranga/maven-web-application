node
{
 def mavenHome = tool name: "maven3.8.4"
 stage('CheckoutCode')
 {
 git branch: 'development', credentialsId: '7d2dc11c-7a6d-4913-b99b-e6c5fdff42ce', url:
 'https://github.com/sayalaranga/maven-web-application.git'
 }
 
 stage('Build'){
 sh "${mavenHome}/bin/mvn clean package"
 }
 
 stage('ExecuteSonarQubeReport'){
 sh "${mavenHome}/bin/mvn clean sonar:sonar"
 }
 
 stage('UploadArtifactIntoNexus'){
 sh "${mavenHome}/bin/mvn clean deploy"
 }
 
 stage('DeployAppintoTomcat'){
 sshagent(['84a5397e-78cc-40f2-9346-7c4d97bd685f']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.234.225.150:/opt/apache-tomcat-9.0.56/webapps/"
 }
 
 }
 
 stage('SendNotifications'){
 emailext body: '''Build over
 Regards
 Bhaskar''', subject: 'Build over', to: 'sayalaranga@gmail.com'
 }
 
}
