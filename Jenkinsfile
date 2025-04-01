pipeline {
    agent any
    
    stages {
        // stage('Docker'){
        //     steps{
        //         sh 'docker build -t my-docker-image .'
        //     }
        // }
        stage('Build') {
            agent {
                docker { 
                    image 'node:22.14-alpine3.20' 
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
                    image 'node:22.14-alpine3.20' 
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
                    image 'node:22.14-alpine3.20' 
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

                    #### Custom docker image

                    netlify --version
                    echo "Deploring to Site ID: $NETLIFY_SITE_ID"
                    netlify status
                    netlify deploy --prod --dir=build
                '''
            }
        }
    }
}

