pipeline {
    agent any

    environment {
        DEV_IMAGE = "gowthamps03/ecommerce-dev:latest"
        PROD_IMAGE = "gowthamps03/ecommerce-prod:latest"
        DOCKERHUB = credentials('dockerhub-creds')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Login') {
            steps {
                sh 'echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_USR --password-stdin'
            }
        }

        stage('Build & Push Dev') {
            when {
                branch 'dev'
            }
            steps {
                sh 'docker build -t $DEV_IMAGE .'
                sh 'docker push $DEV_IMAGE'
            }
        }

        stage('Build & Push Prod') {
            when {
                branch 'master'
            }
            steps {
                sh 'docker build -t $PROD_IMAGE .'
                sh 'docker push $PROD_IMAGE'
            }
        }
    }
}

