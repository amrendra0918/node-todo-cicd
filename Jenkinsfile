pipeline{
    agent { label "dev-server"}
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/amrendra0918/node-todo-cicd" , branch: "master"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t node-app-test-by-amar"
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
               withCredentials([usernamePassword(credentialsId:"DockerHub_LatestCredential",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
               sh "docker tag node-app-test-by-amar ${env.dockerHubUser}/node-app-test-by-amar:latest"
               sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
               sh "docker push ${env.dockerHubUser}/node-app-test-by-amar:latest"
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
