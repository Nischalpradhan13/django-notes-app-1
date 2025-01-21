@Library("Shared") _
pipeline {
    agent { label "Alma" }
    
    stages {
        stage("Library Function") {
            steps {
                script {
                    hello() // Assuming the "hello()" function is defined in your shared library
                }
            }
        }
        stage("Code") {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
                echo "Code cloned successfully"
            }
        }
        stage("Build") {
            steps {
                script{
                echo "Building the Docker image"
                docker_build("note-app", "latest", "nischalpdh")
                }
            }
        }
        stage("Push To Docker Hub") {
            steps {
                script{
                    docker_push("notes-app", "latest", "nischalpdh")
                }
            }
        }
        stage("Deploy") {
            steps {
                echo "Deploying the app"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}
