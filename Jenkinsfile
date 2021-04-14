node {
    def app
    def mvnHome = tool 'Maven'
    stage('Checkout') {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'jenkins_github', url: 'https://github.com/pa1kumarbh/reactive-eventservice']]])
    }
    
    stage('Code quality') {
        withSonarQubeEnv('sonarserver') {
        sh "${mvnHome}/bin/mvn sonar:sonar -f /var/lib/jenkins/workspace/ci-cd/pom.xml"
        }
    }
    

		// Mark the code checkout 'stage'....
		stage('Checkout') {
			checkout scm
		}


		// Build and Push to ACR 'stage'... 
		stage('Build and Push to Azure Container Registry') {
			app = docker.build('demodevsecops.azurecr.io/event-service')
			docker.withRegistry('https://demodevsecops.azurecr.io', 'acr-credentials') {
				app.push("${env.BUILD_NUMBER}")
				app.push('latest')
			}
		}

   
}
