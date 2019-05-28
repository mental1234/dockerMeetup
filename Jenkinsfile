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
  stage('Docker list machines'){
    def masterIP = script(sh 'docker-machine ls | grep master | grep -v grep | awk '{print $5}' | sed 's#tcp://##g' | cut -d\: -f1')
    echo masterIP
  }
}
