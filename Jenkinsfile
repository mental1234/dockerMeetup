pipeline {
    agent any
    parameters {
      booleanParameter(defaultValue: true, description: 'Test paramenter', name: 'Test')
    }
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
