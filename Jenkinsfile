
pipeline {
    agent any
    tools{
         maven 'LocalMaven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Abdul1097/devops-integration']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                bat 'docker build -t javatechie/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                bat 'docker login -u abdul1097 -p ${dockerhubpwd}'
}
                bat 'docker push javatechie/devops-integration'
                }
            }
        }

        
        
    }
}
