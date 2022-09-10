pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
     environment {
    registry = '336743173671.dkr.ecr.ap-south-1.amazonaws.com/geolocation_ecr_rep'
    registryCredential = 'jenkins-ecr'
  }
    stages {
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/philgithub2/geolocation-1.git'
            }
        }
        stage('Code Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
         // Building Docker images
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        // Uploading Docker images into AWS ECR
        stage('Pushing to ECR') {
            steps{
                script {
                    sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin account_id.dkr.ecr.us-east-2.amazonaws.com'
                    sh 'docker push account_id.dkr.ecr.us-east-2.amazonaws.com/my-docker-repo:latest'
                }
            }
        } 
    }
}