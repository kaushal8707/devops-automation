pipeline {
    agent any
    tools{
        maven 'maven3.8.8'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kaushal8707/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                sh 'docker build -t dockerjimaihu/devops-integration .'    
                }
                
            }
        }
         stage('Push Image to Hub'){
            steps{
                script{
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhub-pwd')]) {
                sh 'docker login -u dockerjimaihu -p ${dockerhub-pwd}' 
                sh 'docker push dockerjimaihu/devops-integration'
                 }
            }
                
            }
        }
    }
}