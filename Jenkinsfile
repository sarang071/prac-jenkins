pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = '01'
        DOCKERHUB_REPO = 'sarangp007/sample-nginx-qa' 

    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def commitId = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
                    def imageName = "${env.DOCKERHUB_REPO}:${commitId}"

                    sh "docker build -t ${imageName} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    def commitId = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
                    def imageName = "${env.DOCKERHUB_REPO}:${commitId}"

                    withCredentials([usernamePassword(credentialsId: env.DOCKERHUB_CREDENTIALS, usernameVariable: 'sarangp007', passwordVariable: 'timers123')]) {
                        sh "echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin"
                        sh "docker push ${imageName}"
                    }
                }
            }
        }
    }
}
