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
        stage("Var") {
            steps {
                sh 'echo ${params.Nodes}'
            }
        }
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
