pipeline {
   agent any
   environment {
       DOCKERHUB_CREDENTIALS = credentials('dockerHub')
    }
   stages {
        stage('Checkout') {
            steps {
               git branch: 'main', credentialsId: 'github', url: 'https://github.com/Omprakashsurwase/project1.git'
                sh "ls -lart ./*"
            }
        } 
         stage('Build-Image'){
            steps {
                sh "docker build -t omprakashsurwase/tomcatomimage:v1.$BUILD_ID ."
            }
         }
 stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push omprakashsurwase/tomcatomimage:v1.$BUILD_ID'
            }
        }
        stage('Deploy application on kubernetes container'){
            steps{
                sh 'kubectl apply -f deployment.yml'
            }
        }
    }
}
