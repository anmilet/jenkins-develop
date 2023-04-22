pipeline {
    agent any
    environment{
        GITHUB_CREDENTIALS = credentials('GITHUB_CREDENTIALS')
        DOCKER_HUB_LOGIN = credentials('DOCKER_HUB_CREDENTIALS')
        REGISTRY_USR = "anmilet"
        VERSION = "1.0.0"
        IMAGE = "image-node"
    }
    stages {
        stage('init') {
            agent{
                docker {
                    image 'node:alpine'
                    args '-u root:root'
                }
            }
            steps {
                echo 'install dependencies'
                sh 'npm install'
            }
        }
        stage('test') {
            agent{
                docker {
                    image 'node:alpine'
                    args '-u root:root'
                }
            }
            steps {
                echo 'install dependencies'
                sh 'npm run test'
            }
        }
        stage('Build') {
            steps {
                echo 'listar'
                sh 'docker build -t $IMAGE:$VERSION .'
                sh 'docker images'
            }
        }
        stage('deploy') {
            steps {
                echo 'login'
                sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
                sh 'docker tag $IMAGE:$VERSION $REGISTRY_USR/$IMAGE:$VERSION'
                sh 'docker push $REGISTRY_USR/$IMAGE:$VERSION'

            }
        }
        stage('notification') {
            steps {
                echo 'Hello World'
            }
        }
    }
}