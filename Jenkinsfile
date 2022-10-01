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
                bat 'docker login --username christineibrahim --password dckr_pat_GcIieZugRQS5m7sEpNNqFdJRFxA'
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