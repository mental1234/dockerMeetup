node('master'){
	stage('Create nodes'){
    withCredentials([string(credentialsId: 'DO_TOKEN', variable: 'SECRET')]) {
      sh '''
        for i in `seq 1 ${NodeNumber}`; do
          echo "Creating node $i" 
          docker-machine create --driver digitalocean --digitalocean-image  ${os} --digitalocean-access-token ${SECRET} node$environment-$i
        done
      '''
    } 
  }
  stage('Init manager'){
    sh '''
      MASTER_IP=$(docker-machine ip node$environment-1)
      eval $(docker-machine env node$environment-1)
      docker swarm init --advertise-addr $MASTER_IP
    '''
  }
  stage('Join rest of nodes'){
    sh '''
      eval $(docker-machine env node$environment-1)
      MANAGER_TOKEN=$(docker swarm join-token -q manager)
      WORKER_TOKEN=$(docker swarm join-token -q worker)
      MASTER_IP=$(docker-machine ip node$environment-1)
      for i in `seq 1 ${NodeNumber}`; do
        if [ $i -eq 1 ]; then
          echo "Miss the master node"
        else 
          WORKER_IP=$(docker-machine ip node$environment-$i)
          eval $(docker-machine env node$environment-$i)
          docker swarm join --token $WORKER_TOKEN --advertise-addr $WORKER_IP $MASTER_IP:2377
        fi
      done
    '''
  }
}
