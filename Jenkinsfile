pipeline {
    agent any

    environment {
        IMAGE = 'yourdockerhubusername/simpleapp'
        TAG = 'latest'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/yourusername/your-repo.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE:$TAG .'
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

