pipeline {
    agent any
    stages {
        stage ("code clone") {
            steps {
                git url: "https://github.com/Hemantjangir53/node-todo.git", branch: "main"
                echo "cloning the code"
            }
        }
        stage ("Build") {
            steps {
                sh "docker build . -t node-todo"
                echo "Build the image"
            }
        }
        stage ("Push to dockerHub") {
           steps{
                    withCredentials([
                        usernamePassword(
                            credentialsId: 'dockerHub',
                            usernameVariable: 'DOCKERHUB_USERNAME',
                            passwordVariable: 'DOCKERHUB_PASSWORD')]){
                                sh "docker tag node-todo ${env.DOCKERHUB_USERNAME}/node-todo:latest"   //image tag
                                sh "docker login -u ${env.DOCKERHUB_USERNAME} -p ${env.DOCKERHUB_PASSWORD}"
                                sh "docker push ${env.DOCKERHUB_USERNAME}/node-todo:latest"    //image name-> <dockerhub_user_name>/image_name
                    }
                    echo "code push"
                }
        }
        stage ("Deploy") {
            steps {
                //sh "docker run -d -p 8000:8000 hemantjangir/node-todo:latest"
                sh "docker-compose down && docker-compose up -d"
                echo "deploy successfully"
            }
        }
    }
}
