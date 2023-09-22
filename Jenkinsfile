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
            stage('Push to Docker Hub') {
               steps {
                 echo "Pushing the image to docker hub"
                    sh "docker tag reddit $DOCKERHUB_CREDENTIALS_USR/node-app-test-new:latest"
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                    sh "docker push $DOCKERHUB_CREDENTIALS_USR/node-app-test-new:latest"
                     }
            }

        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
