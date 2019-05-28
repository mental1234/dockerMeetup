node('master'){
	stage('Checkout'){
		checkout scm
	}
	stage('Create master node'){
    withCredentials([string(credentialsId: 'DO_TOKEN', variable: 'SECRET')]) {
      sh 'docker-machine create --driver digitalocean --digitalocean-image ubuntu-16-04-x64 --digitalocean-access-token ${SECRET} master$environment'
    }
  }
  stage('Create nodes'){
    withCredentials([string(credentialsId: 'DO_TOKEN', variable: 'SECRET')]) {
      sh '''
        echo "Hello ${NodeNumber}"
        for i in {1..$NodeNumber}; do
          echo $i 
          #docker-machine create --driver digitalocean --digitalocean-image  ubuntu-16-04-x64 --digitalocean-access-token ${SECRET} node$environment-$i
        done
          
      '''
    } 
  }
}
