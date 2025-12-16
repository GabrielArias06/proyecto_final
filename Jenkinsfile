pipeline {
    agent any

    environment {
        IMAGE_NAME = "alma8-full"
        IMAGE_TAG = "proyecto-final"
        DOCKERHUB_USER = "yeyo19"
        DOCKERHUB_REPO = "${DOCKERHUB_USER}/${IMAGE_NAME}"
    }

    stages {

        stage('Clonar repositorio') {
            steps {
                echo "Clonando repositorio"
                checkout scm
            }
        }

        stage('Construir imagen') {
            steps {
                echo "Construyendo imagen con docker-compose"
                bat 'docker compose build full'
            }
        }

        stage('Etiquetar imagen') {
            steps {
                echo "Etiquetando imagen"
                bat """
                  docker tag alma8-full:1.0 %DOCKERHUB_REPO%:%IMAGE_TAG%
                """
            }
        }

        stage('Darle push a la imagen') {
            steps {
                echo "Subiendo imagen a Docker Hub"
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat """
                      echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                      docker push %DOCKERHUB_REPO%:%IMAGE_TAG%
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