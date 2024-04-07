pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                echo 'vinhbh start...'
                git 'https://github.com/Vinh1507/jenkins-github'
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t vinhbh/simple_image_jenkins .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // Login to Docker Hub
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                }
                // Push Docker image to Docker Hub
                sh 'docker push vinhbh/simple_image_jenkins'
            }
        }
    }
}
