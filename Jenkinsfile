pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/capstoneprojects/repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Dockerize') {
            steps {
                sh 'docker build -t supertech-app .'
                sh 'docker tag supertechis-app sunestech/supertech-app:latest'
                sh 'docker push sunestech/supertech-app:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8080:8080 sunestech/supertechis-app:latest'
            }
        }
    }
}
