pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('christineibrahim')
    }
    stages {
        stage ('Build') {
            steps {
				print('buildingg')
                sh 'docker-compose -f docker-compose-build.yaml build --parallel'
            }
        }
        stage ('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage ('Push') {
            steps {
				sh 'docker image push christineibrahim/udagram_reverseproxy:latest'
				sh 'docker image push christineibrahim/udagram_apiuser:latest'
				sh 'docker image push christineibrahim/udagram_apifeed:latest'
				sh 'docker image push christineibrahim/udagram_frontend:latest'
            }
        }
    }
    post {
        always {
			sh 'docker logout'
        }
    }
}