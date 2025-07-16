pipeline
{
agent any
tools
{
	maven "maven-3.9.9"
}
triggers {
pollSCM('* * * * *')
}

stages
{
stage('Git checkout')
{
	steps
	{
	git branch: 'development', url: 'https://github.com/santhosh2931/maven-webapplication-project-kkfunda.git'
	}
}
stage('Compile')
{
	steps
	{
	sh "mvn clean compile"
	}
}
stage('Build')
{
	steps
	{
	sh "mvn clean package"
	}
}
stage('SonarQube Report')
{
	steps
	{
	sh "mvn sonar:sonar"
	}
}
stage('Deploy to Nexus')
{
	steps
	{
	sh "mvn clean deploy"
	}
}
stage('Deploy to Tomcat')
{
	steps
	{
	sh """

	curl -u santhu:password \
--upload-file /var/lib/jenkins/workspace/iqoo-declarative-way-PL/target/maven-web-application.war \
"http://13.201.229.176:9090/manager/txt/deploy?path=/maven-web-application&update=true"

	
        """
	}
}

} // stages ending
	
} // pipeline ending
