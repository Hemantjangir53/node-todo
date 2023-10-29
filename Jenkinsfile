pipeline {
    agent any 
    stages {
        stage('clode clone') {
            steps {
                git url: "https://github.com/Hemantjangir53/node-todo.git", branch: "main"
                echo "code cloned successfully"
            }
        }
        stage('Build') {
            steps {
                sh 'docker build . -t node-todo-app'
                echo "code build successfully"
            }
        }
        stage('push to docker Hub') {
            steps {
                withCredentials([
                        usernamePassword(
                            credentialsId: 'dockerHub',
                            usernameVariable: 'DOCKER_USERNAME',
                            passwordVariable: 'DOCKER_PASSWORD')]){
                                
                                sh "docker tag node-todo-app ${env.DOCKER_USERNAME}/node-todo-app:latest"
                                sh "docker login -u ${env.DOCKER_USERNAME} -p ${env.DOCKER_PASSWORD}"
                                sh "docker push ${env.DOCKER_USERNAME}/node-todo-app:latest"
                                
                    }
                
                echo "code push"
            }
        }
        stage('deploy') {
            steps {
                //sh "docker run -d -p 8000:8000 hemantjangir/node-todo-app:latest"
                sh "docker-compose down && docker-compose up -d"
                
                echo "container deploy"
            }
        }
    }
}
