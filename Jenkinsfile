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
                sh 'docker build -t supertechis-app .'
                sh 'docker tag supertechis-app <private_registry>/supertechis-app:latest'
                sh 'docker push <private_registry>/supertechis-app:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8080:8080 <private_registry>/supertechis-app:latest'
            }
        }
    }
}
