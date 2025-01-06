pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'bash scripts/build.sh'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'bash scripts/test.sh'
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    sh 'docker build -t zhantorebazarbayev/cicdimage .'
                }
            }
        }
        stage('Docker Login and Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker_hub_creds_id', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh 'echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin'
                        sh 'docker push zhantorebazarbayev/cicdimage'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
