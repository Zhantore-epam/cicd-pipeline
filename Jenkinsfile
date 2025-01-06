pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    // Running the build script
                    sh 'bash scripts/build.sh'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Running the test script
                    sh 'bash scripts/test.sh'
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    // Building the Docker image
                    sh 'docker build -t zhantorebazarbayev/cicdimage .'
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    // Login to Docker Hub and push the image
                    withDockerRegistry([credentialsId: 'docker_hub_creds_id']) {
                        sh 'docker push zhantorebazarbayev/cicdimage'
                    }
                }
            }
        }
    }
    post {
        always {
            // Cleanup or post-processing tasks, if needed
            echo 'Pipeline finished.'
        }
    }
}
