pipeline {
    agent any
    environment {
         NETLIFY_SITE_ID = "8bbf390f-9777-48da-ba5d-640735d410e3"
         NETLIFY_AUTH_TOKEN = credentials('myToken')
        }
    
    stages {
        
        stage('Build') {
            agent {
                docker { 
                    image 'node:22.14.0-alpine' 
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -la
                    node --version
                    npm -version
                    npm install
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker { 
                    image 'node:22.14.0-alpine' 
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
        stage('Deploy') {
            agent {
                docker { 
                    image 'node:22.14.0-alpine' 
                    reuseNode true
                }
            }
            steps {
                sh '''
                    # npm install netlify-cli
                    # node_modules/.bin/netlify --version
                    # echo "Deploring to Site ID: $NETLIFY_SITE_ID"
                    # node_modules/.bin/netlify status
                    # node_modules/.bin/netlify deploy --prod --dir=build 
                '''
            }
        }
    }
}

