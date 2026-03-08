pipeline {

 agent any

 stages {

 stage('Clone Repository') {

 steps {
 git 'https://github.com/gayaskhan1/jenkins-docker-ci-cd.git'
 }

 }

 stage('Build Docker Image') {

 steps {
 sh 'docker build -t gayaskhan1/devops-app .'
 }

 }

 stage('Push Docker Image') {

 steps {
 sh 'docker push gayaskhan1/devops-app'
 }

 }

 stage('Deploy Container') {

 steps {
 sh '''
 docker stop devops-container || true
 docker rm devops-container || true
 docker run -d -p 80:3000 --name devops-container gayaskhan1/devops-app
 '''
 }

 }

 }

}
