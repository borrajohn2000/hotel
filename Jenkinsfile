pipeline {
    agent any

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
                // ✅ FIXED: only one colon in tag
                sh 'docker build -t borrajohn/hotel:1999 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'DOCKER_CREDS']) {
                    sh 'docker push borrajohn/hotel:1999'
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:8080 borrajohn/hotel:1999'
            }
        }
    }
}
