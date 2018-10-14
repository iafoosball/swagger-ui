pipeline {

    agent any
    environment {
        COMPOSE_PROJECT_NAME = "${env.JOB_NAME}-${env.BUILD_ID}"
        COMPOSE_FILE = "docker-compose.yml"
    }
    stages {
        stage ("Prepare Environment") {
            steps {
                sh "cp /var/lib/iafoosabll/swagger-ui/* ./apis/"
            }
        }
        stage ("Build") {
            steps {
            sh "docker-compose up --build"
            }
        }
        stage ("Deploy") {
            steps {
                sh "docker-compose up"
                }
            }
        }
    post {
        always {
            sh "docker-compose down -v"
        }
    }
}