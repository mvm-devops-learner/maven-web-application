
node
{
	echo "The Node name is : ${env.NODE_NAME} "
    def mavenHome=tool name:"maven3.8.5"
stage('CheckoutCode')
{
 git branch: 'development', credentialsId: '8473ea25-caee-4d65-9565-11989734ab87', url: 'https://github.com/mvm-devops-learner/maven-web-application.git'
 
}

stage('Build')
{
       sh "$mavenHome/bin/mvn clean package"
}
stage('sonarQubeReport')
{
	sh "$mavenHome/bin/mvn sonar:sonar"
}

stage('NexusReport')
{
	sh "$mavenHome/bin/mvn deploy"
}

stage('DeployontoTomcat')
{
 sshagent(['f2f757ce-442b-4dc9-9db9-e5a8f8ca7c35']) 
 {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.33.29:/opt/apache-tomcat-9.0.59/webapps"
   }
    
}


}
