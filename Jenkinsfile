pipeline{
    agent any
    tools {
        maven 'maven_3_9_9'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Sachintha1994/simpleProject']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t sachintha94/spring-boot-docker -f DockerFile .'
                }
            }
        }
        stage('Push image to docker hub'){
            steps{
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u sachintha94 -p ${dockerhubpwd}'
                }
                sh 'docker push sachintha94/spring-boot-docker:latest'
            }
        }
    }
}