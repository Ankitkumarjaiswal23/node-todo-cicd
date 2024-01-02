pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: 'https://github.com/Ankitkumarjaiswal23/node-todo-cicd.git' , branch: 'master'
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t node-app-demo"
            }
        }
        stage("Push to Repository") {
    steps {
        withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker tag node-app-demo ${env.dockerHubUser}/node-app-demo:latest"
            sh "docker push ${env.dockerHubUser}/node-app-demo:latest"
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
