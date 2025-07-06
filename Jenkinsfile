pipeline {
    agent any

    environment {
        IMAGE = 'sidd1810/simpleapp'
        TAG = 'v1'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/sidd1810/tata.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t sidd1810/simple:v1 .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE:$TAG'
            }
        }
    }
}

