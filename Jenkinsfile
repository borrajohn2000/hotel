pipeline {
    agent any

    environment {
        IMAGE_NAME = "borrajohn/hotel"
        IMAGE_TAG  = "1999"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/borrajohn2000/hotel.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                // ✅ FIXED TAG (only one colon)
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'DOCKER_CREDS']) {
                    sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:8080 $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }
}
