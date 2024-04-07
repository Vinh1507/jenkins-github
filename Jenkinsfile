pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = 'docker-hub-credentials'
        DOCKER_IMAGE_NAME = 'vinhbh/simple_image_jenkins'
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
                    // Xây dựng Docker image từ Dockerfile
                    def dockerImage = docker.build(env.DOCKER_IMAGE_NAME, '-f .')
                    if (dockerImage != null) {
                        echo 'Docker image đã được xây dựng thành công.'
                    } else {
                        error 'Không thể xây dựng Docker image.'
                    }
                }
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
