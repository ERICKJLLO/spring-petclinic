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
    }
}