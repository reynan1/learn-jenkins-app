pipeline {
    agent any

    environment {
        INDEX_FILE = 'index.html'
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
                     node  --version
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
                echo 'Testing application start...'
                sh '''
                      test -f build/$INDEX_FILE 
                      npm test
                   ''' 
                 echo '...Testing application FINISH...'   
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }

}