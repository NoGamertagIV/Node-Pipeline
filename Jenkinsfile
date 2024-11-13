pipeline {
    agent any

    environment {
        BUILD_FILE_NAME = 'laptop.txt'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            steps {
                
                echo 'Building a new laptop ...'
                
                sh '''
                   ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                 script {
            sh 'ls -R' // Lists all files to confirm file structure
        }
                sh '''
                    test -f public/index.html
                    npm test
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'build/**'
        }
    }
}
