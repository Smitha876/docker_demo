pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" build -t myapp .'
            }
        }

        stage('Tag Image') {
            steps {
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" tag myapp smitha876/myapp:v1'
            }
        }

        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
                usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    
                    bat 'echo %PASS% | "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" login -u %USER% --password-stdin'
                    
                    bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" push smitha209/myapp:v1'
                }
            }
        }
    }
}