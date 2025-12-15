pipeline {
    agent any

    environment {
        IMAGE_NAME = "alma8-full"
        IMAGE_TAG = "proyecto-final"
        DOCKERHUB_USER = "yeyo19"
        DOCKERHUB_REPO = "${DOCKERHUB_USER}/${IMAGE_NAME}"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Clonando repositorio"
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Construyendo imagen con docker-compose"
                sh 'docker compose build full'
            }
        }

        stage('Tag Image') {
            steps {
                echo "Etiquetando imagen"
                sh """
                  docker tag alma8-full:1.0 ${DOCKERHUB_REPO}:${IMAGE_TAG}
                """
            }
        }

        stage('Push Image') {
            steps {
                echo "Subiendo imagen a Docker Hub"
                withCredentials([usernamePassword(
                    credentialsId: 'proyecto final',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                      echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin
                      docker push ${DOCKERHUB_REPO}:${IMAGE_TAG}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Imagen construida y subida correctamente"
        }
        failure {
            echo "Fallo en el pipeline"
        }
    }
}