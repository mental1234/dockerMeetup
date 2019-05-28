node('master'){
	stage('Checkout'){
		checkout scm
	}
	stage('Main Deploy'){
        sh 'echo ${region} ${environment}'
    }
}
