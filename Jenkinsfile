pipeline{
    
    agent any;
    
    stages{
      stage("code clone"){
         steps{
          git url:"https://github.com/Arshiya0123/two-tier-flask-app.git",branch:"master"
      }  
    }
     stage("build"){
         steps{
             sh "docker build -t flask-app ."
         }
     } 
     stage("test"){
         steps{
         echo "tester will be done"
         
         }
     }
     stage("push to dockerhub"){
         steps{
             withCredentials([usernamePassword(
                credentialsId:"dockerHubCreds",
                passwordVariable: "dockerHubPass",
                usernameVariable: "dockerHubUser"
             )]){
             sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
             sh "docker image tag flask-app ${env.dockerHubUser}/my-flask"
             sh "docker push ${env.dockerHubUser}/my-flask:latest"
             
              }
            } 
         } 
       stage("deploy"){
           steps{
               sh "docker-compose up -d --build flask-app"

           }
       }  
     } 
     post{
         success{
             script{
                 email text from:'gmail',
                     to:'gmail',
                     body:'Build success for First cicd',
                     subject:'Build success'

             }
         }
     }
    }   
