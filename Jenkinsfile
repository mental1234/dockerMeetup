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
        for i in `seq 1 ${NodeNumber}`; do
          echo "Creating node $i" 
          docker-machine create --driver digitalocean --digitalocean-image  ubuntu-16-04-x64 --digitalocean-access-token ${SECRET} node$environment-$i
        done
      '''
    } 
  }
  stage('Cluster'){
    sh 'echo "hello" '
    sh '''
      MANAGER_IP=`docker-machine ip master$environment`
      docker swarm init --advertise-addr $MANAGER_IP --listen-addr 127.0.0.1
      eval $(docker-machine env master$environment)
      
      MANAGER_TOKEN=`docker swarm join-token -q manager`
      WORKER_TOKEN=`docker swarm join-token -q worker`
    
      for i in `seq 1 ${NodeNumber}`; do
        WORKER_IP=`docker-machine ip node$environment-$i`
        docker swarm join --token $WORKER_TOKEN --advertise-addr $WORKER_IP $MANAGER_IP:2377
      done
    '''
    }
  stage('Final Step'){
    sh 'docker-machine ls'
    sh 'docker node ls'
  }
}
