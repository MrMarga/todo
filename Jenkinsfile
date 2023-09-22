pipeline {
    agent any
    environment{DOCKERHUB_CREDENTIALS = credentials('dockerhublogin')}
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/MrMarga/todo.git", branch: "master"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t node-app-test-new"
            }
        }
        stage("Push to DockerHub"){
            steps{
               {
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                    sh "docker tag node-app-test-new $DOCKERHUB_CREDENTIALS_USR/node-app-test-new:latest"
                    sh "docker push $DOCKERHUB_CREDENTIALS_USR/node-app-test-new:latest" 
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
