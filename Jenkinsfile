pipeline {
    agent any
    parameters {
      booleanParam(defaultValue: true, description: 'Test paramenter', name: 'Test')
      string(defaultValue: '5', description: 'Number of nodes', name: 'Nodes')
    }
    stages {
        stage("foo") {
            steps {
                echo "flag: ${params.Test}"
            }
        }
        stage("Creation of master node") {
            steps {
                sh "echo 'Docker master creating...' "
                sh ""
            }
        }
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
