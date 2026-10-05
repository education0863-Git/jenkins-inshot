@Library('shared@main') _
pipeline {
    agent { label "vinod" }
    
    stages {
        stage("hello") {
            steps {
                script {
                    hello()
                }
            }
        }
        stage("code") {
            steps {
                script {
                   gitclone("https://github.com/education0863-Git/jenkins-inshot.git", "main")
                }
            }
        }
        stage("Build") {
            steps {
                script {
                    docker_build("notes-app", "latest", "dockerpractice123456/notes-app:latest")
                }
            }
        }
        stage("push to DockerHub") {
            steps {
                script {
                    docker_push("dockerpractice123456/notes-app:latest")
                }
            }
        }
        stage("Deploy") {
            steps {
                echo "This is deploying the code"
                sh "docker ps -q --filter publish=8000 | xargs -r docker rm -f || true"
                sh "docker compose up -d"
            }
        }
    }
}
