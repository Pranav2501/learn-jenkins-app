pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '28c70179-3b06-46b8-9f81-df6515898d63'
    }
    stages {
        
        stage('Build') {
            agent {
                    docker {
                        image 'node:18-alpine'
                        reuseNode true
                     }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    echo "Installing dependencies..."
                    npm ci
                    echo "Building the project..."
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    echo "Running tests..."
                    test -f build/index.html && echo "File exists" || echo "File does not exist"
                    npm test
                '''
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Deploying the project..."
                    npm install netlify-cli -g
                    echo "SITE_ID: $NETLIFY_SITE_ID"

                '''
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
