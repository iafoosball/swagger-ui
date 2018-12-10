pipeline {

    agent any
    environment {
        COMPOSE_PROJECT_NAME = "${env.JOB_NAME}-${env.BUILD_ID}"
        COMPOSE_FILE = "docker-compose.yml"
    }
    stages {
        stage ("Prepare Environment") {
            steps {
                sh "mkdir apis &"
                sh "cp -rf /var/lib/iafoosball/openAPISpecs/* ./apis/ &"
            }
        }
        stage ("Build") {
            steps {
                sh "docker stop swagger &"
                sh "sleep 30s"
                sh "docker-compose build"
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
