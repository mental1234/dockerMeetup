node('master'){
	stage('Checkout'){
		checkout scm
	}
	stage('Create master node'){
    withCredentials([string(credentialsId: 'DO_TOKEN', variable: 'SECRET')]) {
      sh 'docker-machine create --driver digitalocean --digitalocean-image ubuntu-16-04-x64 --digitalocean-access-token ${SECRET} master$environment'
      sh 'eval $(docker-machine env master$environment)'
    }
  }
  stage('Create nodes'){
    withCredentials([string(credentialsId: 'DO_TOKEN', variable: 'SECRET')]) {
      sh '''
        MANAGER_IP=`docker-machine ip master$environment`
        echo $MANAGER_IP
        for i in `seq 1 ${NodeNumber}`; do
          echo "Creating node $i" 
          docker-machine create --driver digitalocean --digitalocean-image  ubuntu-16-04-x64 --digitalocean-access-token ${SECRET} node$environment-$i
        done
      '''
    } 
  }
}
