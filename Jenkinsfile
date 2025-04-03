pipeline {
    agent any
    environment {
         NETLIFY_SITE_ID = "a95661ed-2322-48f9-bac6-c431ff879ec6"
         NETLIFY_AUTH_TOKEN = credentials('myToken')
     }
    
    stages {
        // stage('Docker'){
        //     steps{
        //         sh 'docker build -t my-docker-image .'
        //     }
        // }
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

