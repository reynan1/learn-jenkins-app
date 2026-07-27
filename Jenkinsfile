pipeline {
    agent any

    environment {
        INDEX_FILE = 'index.html'
    }

    stages {
        /*
         line 1 
         line 2   
        */
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

        stage('E2E') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'E2E testing application start...'
                sh '''
                      npm run build
                      npm install -g serve
                      serve -s build
                   ''' 
                 echo '...E2E testing application finish...'   
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }

}