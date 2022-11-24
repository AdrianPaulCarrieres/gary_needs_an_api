pipeline {
    agent any

    tools {
        nodejs "node 18"
    }

    stages {
        stage('Git checkout') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'test', url: 'https://github.com/AdrianPaulCarrieres/efrei2022-gary_needs_an_api'
            }
        }
        stage('github webhook stage') {
            steps {
                sh 'l -ali'
            }
        }
        stage('NPM install') {
            steps {
                sh 'npm install'
            }
        }
        stage('NPM test') {
            steps {
                sh 'npm run test'
            }
        }
        stage('DOCKER build') {
            steps {
                sh "docker build -t adrianpaulcarrieres/garry:latest '.'"
            }
        }
    }
    post {
        failure {
            emailext body: 'Ce build $BUILD_NUMBER a échoué',
                     recipientProviders: [requestor()], 
                     subject: 'build',
                     to: 'adrian-paul.carrieres@efrei.net'
        }
    }
}
