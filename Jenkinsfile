pipeline {
    agent any
    parameters {
      choice(choices: ['Dev', 'Stg'], description: 'Environment', name: 'Environment')
      string(defaultValue: '5', description: 'Number of nodes', name: 'Nodes')
    }
    environment { 
        DOTOKEN = credentials('DO_TOKEN') 
    }
    stages {
        stage("Creation of master node") {
            steps {
                sh "echo 'Docker master creating...' $Environment "
                sh '''
                    docker-machine create --driver digitalocean --digitalocean-image ubuntu-16-04-x64 --digitalocean-access-token $DOTOKEN node2
                   '''
            }
        }
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
