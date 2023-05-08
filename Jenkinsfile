pipeline{
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/galai11/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    bat "docker build -t galaijihed/devops-integration ."
                }
            }
        }
        stage('Push Docker Image to Docker Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'passwordDockerHub', variable: 'password-docker-hub')]) {
                       // bat 'docker login -u galaijihed -p $password-docker-hub '
                        bat 'docker login -u galaijihed -p %password-docker-hub%'
}
                        bat 'docker push galaijihed/devops-integration'

                }

            }
        }
    }

}