pipeline{
    agent any
    stages{
        stage("code clone"){
            steps{
                git url:"https://github.com/aniketware25/node-todo-cicd.git" , branch:"master"
                
            }
        }
        stage("code build and test"){
            steps{
                sh "docker build . -t node-app:latest"
            }
        }
        stage("copy to dockerHub"){
             steps{
                 withCredentials([usernamePassword(credentialsId:"dockerHub",usernameVariable:"dockerUser",passwordVariable:"dockerPass")]){
                     sh "docker login -u ${env.dockerUser} -p ${env.dockerPass} "
                     sh "docker tag node-app ${env.dockerUser}/node-app:latest"
                     sh "docker push ${env.dockerUser}/node-app:latest"
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
