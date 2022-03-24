node('whatsappnode-1'){

def mavenHome = tool name:'Maven-3.8.2',type:'maven'

stage('Git Checkout')
{

git branch: 'development', credentialsId: '8b68e3f7-dbff-4cfd-adb9-fbb643fa15c0', url: 'https://github.com/omsai767/maven-web-application.git'


}

stage('Build Artifact')
{

sh "${mavenHome}/bin/mvn clean package"
}

stage('SonarQube Report')
{

sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('Uploading Artifact into Nexus')
{
sh "${mavenHome}/bin/mvn clean deploy"
}

stage('Tomcat')
{
sshagent(['dee6920d-bbbd-4922-b8da-6e2c71b7a34a'])
{

sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.111.188.147:/opt/apache-tomcat-9.0.60/webapps/"

}
}


stage('Send email mawa')
{
    
emailext body: '''Hi,
Build over ..


thanks,
omsai
''', subject: 'Build over abbai', to: 'meetvenkata22@gmail.com'
}
}
