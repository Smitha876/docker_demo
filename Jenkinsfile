pipeline {
    agent any

    stages {
      stage('Clone') {
        steps {
            git branch: 'main', url: 'https://github.com/Smitha876/docker_demo.git'
        }
    }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp .'
            }
        }

        stage('Tag Image') {
            steps {
                sh 'docker tag myapp yourusername/myapp:v1'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push yourusername/myapp:v1'
                }
            }
        }
    }
}