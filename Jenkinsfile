pipeline {
    agent { label 'dev-agent'}
    
    stages{
        stage('code'){
            steps {
                git url: 'https://github.com/Abhibhagat1407/node-todo-cicd.git/', branch: 'master'
            }
            
        }
        
        stage('build and test'){
            steps {
                sh 'docker build . -t abhishekbhagat/node-todo-app-cicd:latest'
            }
            
        }
        
        stage('login and push image'){
            steps {
                echo "logging in and pushing image...."
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHub_password', usernameVariable: 'dockerHub_username')]) {
                    sh "docker login -u ${env.dockerHub_username} -p ${env.dockerHub_password}"
                    sh 'docker push abhishekbhagat/node-todo-app-cicd:latest'
                }
            }
            
        }
        
        stage('deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
            
        }
        
    }
}
