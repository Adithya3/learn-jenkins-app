pipeline {
    agent any

    stages {

        stage('Unit tests') {
                    agent {
                        docker {
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }

                    steps {
                        sh '''
                            node --version
                            npm --version
                            npm ci
                            #test -f build/index.html
                            npm test
                        '''
                    }

                    post {
                        always{
                            junit 'test-results/junit.xml'
                        }
                    }
                }
 
        
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
                    npm run build
                    ls -la
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
                npm install netlify-cli
                netlify --version
                '''
            }
        }

    }
}