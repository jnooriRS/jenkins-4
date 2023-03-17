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
                sh "docker tag trio-task-flask-app:latest jnoori31/flask-app"
                sh "docker push jnoori31/flask-app"
                sh "docker tag trio-task-mysql:5.7 jnoori31/db"
                sh "docker push jnoori31/db"
            }          
        }
    }
}
