pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('christineibrahim')
    }
    stages {
        stage ('Build') {
            steps {
                bat 'docker-compose -f docker-compose-build.yaml build --parallel'
            }
        }
        stage ('Login') {
            steps {
                bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage ('Push') {
            steps {
				bat 'docker image push christineibrahim/udagram_reverseproxy:latest'
				bat 'docker image push christineibrahim/udagram_apiuser:latest'
				bat 'docker image push christineibrahim/udagram_apifeed:latest'
				bat 'docker image push christineibrahim/udagram_frontend:latest'
            }
        }
    }
    post {
        always {
			bat 'docker logout'
        }
    }
}