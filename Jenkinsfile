pipeline {
    agent any
    tools{
        maven 'M2_HOME'
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
    }
}