pipeline {
    agent {
	    docker {
	        image 'docker:20.10' // Example Docker image with Docker CLI
	        args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
	    }
    }
    stages {
        stage('Build') {
            steps {
                sh 'bash scripts/build.sh'
            }
        }
        stage('Test') {
            steps {
                sh 'bash scripts/test.sh'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t zhantorebazarbayev/cicdimage .'
            }
        }
        stage('Docker Push') {
            steps {
                withDockerRegistry([url: '', credentialsId: 'docker_hub_creds_id']) {
                    sh 'docker push zhantorebazarbayev/cicdimage'
                }
            }
        }
    }
}
