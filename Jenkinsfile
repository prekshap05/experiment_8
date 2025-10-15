pipeline {
    agent any

    environment {
        // Replace 'username' with your DockerHub username
        DOCKER_IMAGE = "prekshapatil/my-web-app"
    }

    stages {

        stage('Checkout') {
            steps {
                // Replace the repo URL below with your actual GitHub repository
                git 'https://github.com/prekshap05/experiment_8.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
                    usernameVariable: 'prekshapatil', passwordVariable: 'Preksha@1528')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh "docker push $DOCKER_IMAGE"
                }
            }
        }

        stage('Deploy Container') {
            steps {
                // Run the container on port 8080 mapped to container port 80
                sh "docker run -d -p 8080:80 --name my-web-app-container $DOCKER_IMAGE"
            }
        }
    }
}
