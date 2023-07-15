pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/udiscopotato/task-4.git'
            }
        }
        stage('build and push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub') {
                        sh "docker build -t udiscopotato/pythonapi:${env.BUILD_NUMBER} ."
                        sh "docker push udiscopotato/pythonapi:${env.BUILD_NUMBER}"
                    }
                }
            }
        }
        stage('run') {
            steps {
                script {
                    sh "docker pull udiscopotato/pythonapi:${env.BUILD_NUMBER}"
                    sh "docker rm -f api"
                    sh "docker run -d -p 3000:7000 --name api udiscopotato/pythonapi:${env.BUILD_NUMBER}"
                }
            }
        }
    }
}
