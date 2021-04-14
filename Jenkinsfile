node {
    def app
    

		// Mark the code checkout 'stage'....
		stage('Checkout') {
			checkout scm
		}


		// Build and Deploy to ACR 'stage'... 
		stage('Build and Push to Azure Container Registry') {
			app = docker.build('demodevsecops.azurecr.io/event-service')
			docker.withRegistry('https://demodevsecops.azurecr.io', 'acr-credentials') {
				app.push("${env.BUILD_NUMBER}")
				app.push('latest')
			}
		}

   
}
