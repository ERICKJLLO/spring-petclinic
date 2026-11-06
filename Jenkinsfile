pipeline {
    agent any

    stages {
        stage('Maven Install') {
            agent {
                docker {
                    image 'maven:3.9-eclipse-temurin-25'
                    reuseNode true
                }
            }
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t erickjllo/spring-petclinic:gestion-udem-jenkins .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerHub',
                        usernameVariable: 'DOCKERHUB_USER',
                        passwordVariable: 'DOCKERHUB_TOKEN'
                    )
                ]) {
                    sh '''
                        set +x
                        set -eu
                        printf '%s' "$DOCKERHUB_TOKEN" | docker login --username "$DOCKERHUB_USER" --password-stdin
                        docker push erickjllo/spring-petclinic:gestion-udem-jenkins
                        docker logout
                    '''
                }
            }
        }
    }
}