node('master'){
	stage('Checkout'){
		checkout scm
	}
	stage('Create master node){
    withCredentials([string(credentialsId: 'DO_TOKEN', variable: 'SECRET')]) {
      sh 'docker-machine create --driver digitalocean --digitalocean-image ubuntu-16-04-x64 --digitalocean-access-token ${SECRET} master$environment'
    }
  }
  stage('Create nodes'){
    sh ' echo "Hello World"'
  } 
}
