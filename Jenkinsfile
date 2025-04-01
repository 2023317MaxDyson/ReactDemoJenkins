pipeline {
    agent any
    environment{
     NETLIFY_SITE_ID = '880c2019-83a8-49c4-bdbf-d1a08d9d285a'
     NETLIFY_AUTH_TOKEN = credentials('myToken')

    }

    stages {
        stage('Build') {
            agent {
                docker { 
                    image 'node:20.11.0-alpine' 
                    reuseNode true
                }
            }
            steps {
                sh ''' 
                ls -la
                node --version
                npm --version
                npm install
                npm run build
                ls -la
                '''
            }
        }
        stage('Test'){
            agent{
                docker{
                    image  'node:20.11.0-alpine' 
                    reuseNode true
                }
            }
            steps{
                sh  '''
                test -f build/index.html
                npm test
                '''
            }
        }
      
    }
}
 
