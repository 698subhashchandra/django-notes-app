@Library("Shared") _
pipeline {
    
    agent { label 'vinod' }

    stages {
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Code') {
            steps {
                script{
                 echo 'This is Cloning the Code'
                 clone'https://github.com/698subhashchandra/django-notes-app.git', 'main'
                 echo 'Code Cloning Done'
                }
            }
        }
        stage('Build') {
            steps {
                script{
                 docker_build('notes-app', 'latest', '698subhashchandra')
                }
            }
        }
        stage('Push the Image') {
            steps {
               script{
                   docker_push('notes-app', 'latest', '698subhashchandra')
               }
            }
        }
        stage('Deploy') {
            steps {
                echo 'This is deploying the code'
                sh 'docker compose down && docker compose up -d'
            }
        }
    }
}

