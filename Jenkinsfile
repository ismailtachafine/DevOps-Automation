pipeline {
    agent any
    tools {
        maven 'maven_3.9.3'
    }
    stages {
        stage('Build Maven'){
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/linuxboii/DevOps-Automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    sh 'docker build -t ismailtachafine/devops-integration2 .'
                }
            }
        }
        stage('Push Image to Dockerhub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u ismailtachafine -p ${dockerhubpwd}'
                    }
                    sh 'docker push ismailtachafine/devops-integration2'
                }
            }
        }
    }
}