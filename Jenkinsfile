pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'Supertech'
        REGISTRY = 'https://hub.docker.com/repository/docker/sunestech'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'GIT-PAT', url: 'https://github.com/sunestech/capstoneprojects.git
                            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                sh 'sonar-scanner -Dsonar.projectKey=your-project-key'
            }
        }
        stage('Package') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
                sh 'docker push $REGISTRY/$DOCKER_IMAGE:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh 'ansible-playbook deploy.yml'
            }
        }
    }
}
