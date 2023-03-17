pipeline {
    agent any
    environment {
        SECRET_VAR = credentials('3')
        DOCKERHUB_CREDENTIALS = credentials('docker')
    }
    stages {
        stage('Init') {
            steps {
                sh 'docker rm -f $(docker ps -qa)'
                sh 'docker network create trio-task-network'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t trio-task-mysql:5.7 db'
                sh 'docker build -t trio-task-flask-app:latest flask-app'
            }
        }
        stage('Deploy') {
            steps {
                sh './deploy.sh'
            }
        }
        stage('Push') {        
            steps {                                  
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"                                  
                sh "docker tag nginx jnoori31/mynginx:latest"
                sh "docker push jnoori31/mynginx:latest"
            }          
        }
    }
}
