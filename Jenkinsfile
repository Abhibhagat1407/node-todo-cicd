pipeline {
    agent { label 'dev-agent' }
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/Abhibhagat1407/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build and testing') {
            steps {
                sh 'docker build . -t abhishekbhagat/node-todo-cicd:latest'
            }
        }
        stage('logging in and pushing image') {
            steps {
                echo "logging in and pushing image"
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push abhishekbhagat/node-todo-cicd:latest"
                }
            }
        }
        stage('deploying') {
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
