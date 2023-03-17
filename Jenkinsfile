pipeline {

    agent any

    environment {

        SECRET_VAR = credentials('3')

        DOCKERHUB_CREDENTIALS=credentials('docker')

    }

    stages {

        stage('Init') {

            steps {

                sh 'docker stop mynginx || true'

                sh 'docker rm mynginx || true'

            }

        }  

        stage('Build') {

            steps {

                sh 'docker run -d -p 80:80 --name mynginx nginx:latest'

                              sh "docker exec mynginx sh -c 'echo \"Hello Jenkins! ${SECRET_VAR}\" > /usr/share/nginx/html/index.html' "

            }

        }

         stage('Push') {        

            steps{                                  

                           sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"                                  

                           echo 'Login Completed'

                sh "docker tag nginx jnoori31/mynginx:latest"

                sh "docker push jnoori31/mynginx:latest"

            }          

        }

    }
}