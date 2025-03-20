pipeline {
    agent any
    environment {
       
    }
    stages {
        
        // stage('Build') {
        //     agent{
        //         docker {
        //             image 'node:22.14.0-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             ls -la 
        //             node --version
        //             npm --version
        //             npm install
        //             npm run build
        //             ls -la 
        //         '''
        //     }
        // }
        // stage('Test') {
        //     agent{
        //         docker{
        //             image 'node:22.14.0-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             test -f build/index.html
        //             npm test
        //         '''
        //     }
        // }
        stage("AWS"){
            agent{
                docker{
                    image 'amazon/aws-cli'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    aws --version
                '''
            }
        }
        
    }
}