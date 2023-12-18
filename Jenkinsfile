node('AppServer')
{
	def app
	stage('Cloning Git')
	{
		/* Let's make sure we have the repository cloned to our workspace */
		checkout scm
	}
	stage('Build-and-Tag')
	{
		/* This builds the actual image and is synonymous to docker build on the command line */
		app = docker.build("caytlin/nodejschatapp:latest")
	}
	stage('Post-to-dockerhub')
	{
		docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
		{
			app.push("latest")
		}
	}
	stage('Pull-Image-Server')
	{
		sh "docker-compose down"
		sh "docker-compose up -d"
	}
}
