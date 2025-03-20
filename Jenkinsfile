pipeline {
    agent any
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
                withCredentials([usernamePassword(credentialsId: 'my-aws-jenkins', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')])
                 {
                    sh '''
                        aws --version
                        aws s3 ls 
                    '''
                }
            }
        }
        
    }
}