node('master'){
	stage('Checkout'){
		checkout scm
	}
	stage('Main Deploy'){
	    
        withCredentials([string(credentialsId: 'DO_TOKEN', variable: 'SECRET')]) {
            sh 'docker-machine create --driver digitalocean --digitalocean-image ubuntu-16-04-x64 --digitalocean-access-token ${SECRET} master$environment'
        }
    }
}
