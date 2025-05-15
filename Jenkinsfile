pipeline {
    agent any

    stages {
        stage('w/0 docker') {
            steps {
                sh '''
                    echo "Hello World"
                    ls -la
                    touch container-no.txt
                '''
                
                
            }
        }
        stage('with docker') {
            agent {
                    docker {
                        image 'node:18-alpine'
                        reuseNode true
                     }
            }
            steps {
                sh '''
                    echo "Hello World"
                    ls -la
                    touch container-yes.txt
                '''
            }
        }
    }
}
