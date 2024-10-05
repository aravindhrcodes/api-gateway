pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/AryanKulathinal/project1-api-gateway.git', branch: 'main'
            }
        }
        stage('Pre_Build'){
            steps {
                bat "docker rm -f gateway_container"
                bat "docker rmi -f gateway_image"
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {

                bat "docker build -t gateway_image ."
                bat "docker run -p 8060:8060 -d --name gateway_container gateway_image"
            }
        }
    }
}
