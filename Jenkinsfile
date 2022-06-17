pipeline {
    agent any

    stages {

        stage('Delete workspace before build starts') {
            steps {
                echo 'Deleting workspace'
                deleteDir()
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/svdevops07/deploy_to_kubernetes.git'
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -f ./nginx-html/Dockerfile -t svdevops07/kuber_app:v0.1 .'
            }
        }

        stage('Docker run') {
            steps {
                sh 'docker stop kuber_app'
                sh 'docker rm kuber_app'
                sh 'docker run --name kuber_app -d -p 8081:80 svdevops07/kuber_app:v0.1'
            }
        }
    }
}