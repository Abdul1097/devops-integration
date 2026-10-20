
pipeline {
    agent any

    tools {
        maven 'maven_3.9.9'
    }

    stages {
        stage('Build Maven') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    extensions: [],
                    userRemoteConfigs: [[
                        url: 'https://github.com/Abdul1097/devops-integration'
                    ]]
                ])

                bat 'mvn clean install'
            }
        }

        stage('Build docker image') {
            steps {
                bat 'docker build -t abdul1097/devops-integration:latest .'
            }
        }

       stage('Push image to Hub') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'dockerhub-pwd',
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_PASS'
        )]) {
            bat '''
                echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                docker push abdul1097/devops-integration
            '''
        }
    }
    }
}
}
