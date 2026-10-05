pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Arosmith-S/Aro.portfolio.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t aro-portfolio:%BUILD_NUMBER% .'
                bat 'docker tag aro-portfolio:%BUILD_NUMBER% aro-portfolio:latest'
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                    docker stop aro-portfolio
                    docker rm aro-portfolio
                    docker run -d --name aro-portfolio -p 8080:80 aro-portfolio:latest
                '''
            }
        }
    }
}
