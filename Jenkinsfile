pipeline {
    agent any
    parameters {
      booleanParameter(defaultValue: true, description: 'Test paramenter', name: 'Test')
    }
    stages {
        stage("foo") {
            steps {
                echo "flag: ${params.Test}"
            }
        }
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
