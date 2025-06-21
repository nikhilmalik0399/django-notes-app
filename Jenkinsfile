@Library('Shared')_
pipeline{
    agent { label 'Nikhil'}
    
    stages{
        stage("hello"){
            script{
                hello()
            }
        }
        stage("Code clone"){
            steps{
                sh "whoami"
                script{
                     clone("https://github.com/nikhilmalik0399/django-notes-app.git", "main")
                }
            }
        }
        stage("Code Build"){
            steps{
            docker build -t notes-app:latest .
            }
        }
        stage("Push to DockerHub"){
            steps{ 
               withCredentials(usernamePassword[credentialsId: 'dockerCred', passwordVariable:'dockerhubPass', usernameVariable:'dockerHubUser']){
                   docker login -u ${env.dockerHubUser} -p ${env.dockerhubPass}
                   sh " docker push ${dockerHubUser}/notes-app:latest
            }
        }
        stage("Deploy"){
            steps{
               sh "docker compose up -d"
            }
        }
        
    }
}
