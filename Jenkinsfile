pipeline {
    agent any
    environment {
        SECRET_VAR = credentials('3')
        DOCKERHUB_CREDENTIALS = credentials('docker')
    }
    stages {
    
        stage('Deploy') {
    steps {
        sh 'chmod +x ./deploy.sh'
        sh './deploy.sh'
    }
        }
        stage('Push') {        
            steps {                                  
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"                                  
                sh "docker tag trio-task-flask-app:latest flask-app"
                sh "docker push trio-task-flask-app:latest flask-app"
                sh "docker tag trio-task-mysql:5.7 db"
                sh "docker push trio-task-mysql:5.7 db"
            }          
        }
    }
}
