pipeline{
    agent{ label "binod"}
    stages{
        stage("Code"){
             steps{
                 echo "this is cloning the code"
                 git url: "https://github.com/Tejash-TS/django-notes-app.git",branch:"main"
                  echo "code clone successfully"
             } 
        }
        stage("Build"){
              steps{
                  echo "this is building the code"
                  sh "docker build -t notes-app:latest ."
              }
        }
        stage("Push To DockerHub"){
             steps{
                  echo "pushing the image to docker hub"
                  withCredentials([
                      usernamePassword(
                          credentialsId:"dockerHubCred",
                          passwordVariable:"dockerHubPass",
                          usernameVariable:"dockerHubUser")]){
                  sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"     //"-u tejash727 -p myPW"
                  sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                  sh "docker push ${env.dockerHubUser}/notes-app:latest"
             }   }
        }
        stage("Deploy"){
              steps{
              echo "this is deploying the code"
              sh "docker compose up -d"

              }
        }
    }
}
