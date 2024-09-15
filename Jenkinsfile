pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning Repository......'
                git branch: 'main', url: 'https://github.com/glazedonuts616/CI-CD_Proj.git'
            }
        }
    
        stage('List Files') {
           steps {
                sh 'ls -al'
        }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo 'building image....'
                    app=docker.build("glazedonuts616/flask-contacts-app:3.0", '-f FLASK-CONTACTS-DEVOPS/Dockerfile FLASK-CONTACTS-DEVOPS')
                }
            }
        }
        stage('Login') {
            steps {
                script {
                    echo 'loging into dockers and github....'
                    withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    }
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    echo 'Pushing into DockerHub'
                        docker.withRegistry('https://index.docker.io/v1/', 'docker-credentials') {
                            app.push('4.0')
                    }
                }
            }
        }
        stage('Deploy with Docker Compose') {
            steps {
                 dir('FLASK-CONTACTS-DEVOPS') {
                        sh 'docker-compose up -d'
                    }
        }
    }
}
}