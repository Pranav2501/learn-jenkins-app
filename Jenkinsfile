pipeline {
    agent any

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
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
