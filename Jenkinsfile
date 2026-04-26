pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myapp .'
            }
        }

        stage('Tag Image') {
            steps {
                bat 'docker tag myapp smitha876/myapp:v1'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                    bat 'docker push smitha876/myapp:v1'
                }
            }
        }
    }
}