pipeline {
    agent any

    stages {

        stage('First') {
            steps {
                sh 'docker ps'
            }
        }

        stage('Second') {
            steps {
                sh 'docker build -t vivekthanth1/python1:latest .'
            }
        }

        stage('Third') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'username',
                        passwordVariable: 'password'
                    )
                ]) {
                    sh '''
                    docker login -u ${username} -p ${password}
                    docker push vivekthanth1/python1:latest
                    '''
                }
            }
        }

        stage('Fourth') {
            steps {
                sh 'docker run -d -p 5000:5000 --name python1-container vivekthanth1/python1:latest'
            }
        }
    }
}
