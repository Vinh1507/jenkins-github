pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = 'dockerhub_vinhbh'
        registry = 'vinhbh/simple_image_jenkins'
    }
    stages {
        stage('Clone') {
            steps {
                script {
                    echo 'vinhbh start...'
                    // Clone code from a specific branch
                    git branch: 'main', url: 'https://github.com/Vinh1507/jenkins-github'
                }
            }
        }
        stage('Build Image') {
            steps {
                script {
                    docker.build('vinhbh/simple_image_jenkins:1.0', '.')
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // Login to Docker Hub
                withCredentials([usernamePassword(credentialsId: 'dockerhub_vinhbh', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                }
                // Push Docker image to Docker Hub
                sh 'docker push vinhbh/simple_image_jenkins:1.0'
            }
        }
    }
}
