@Library('Shared')_
pipeline {
    agent { label 'nikhil' }

    stages {
        stage("hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage("Code clone") {
            steps {
                sh "whoami"
                script {
                    clone("https://github.com/nikhilmalik0399/django-notes-app.git", "main")
                }
            }
        }

        stage("Code Build") {
            steps {
                sh 'docker build -t notes-app:latest .'
            }
        }

        stage("Push to DockerHub") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerCred', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerhubPass')]) {
                    sh 'docker login -u ${dockerHubUser} -p ${dockerhubPass}'
                    sh 'docker push ${dockerHubUser}/notes-app:latest'
                }
            }
        }

        stage("Deploy") {
            steps {
                sh "docker compose up -d"
            }
        }
    }
}

