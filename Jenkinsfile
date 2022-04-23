pipeline {
    agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred')
	}

    stages {
        stage('Build') {
            steps {
                // sh 'git clone '
                sh 'git clone https://github.com/lazarevtill/TestJenkins.git && cd TestJenkins'

                                sh "ls -la"
                // sh 'cd TestJenkins'
                
                // sh "ls -la"
                // sh 'cd TestJenkins'
                // sh "ls -la"
                sh "docker build --tag testjenkins -f /Dockerfile"
            }
        }
        stage('Login') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {
			steps {
				sh 'docker push lazarevtill/testjenkins:latest'
			}
		}
	}

	    post {
	    	always {
	    		sh 'docker logout'
	    	}
	    }
}
