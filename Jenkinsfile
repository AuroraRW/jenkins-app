pipeline {
    agent any
    stages {
        
        // stage('Build') {
        //     agent {
        //         docker {
        //             image 'node:22-alpine'
        //             // for the same docker image, reuse
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             # list all files
        //             ls -la
        //             node --version
        //             npm --version
        //             # npm install
        //             npm ci
        //             npm run build
        //             ls -la
        //         '''
        //     }
        // }

        // stage('Test') {
        //     agent {
        //         docker {
        //             image 'node:22-alpine'
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
        stage('AWS') {
            agent {
                docker {
                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrypoint=""'
                }
            }
            // environment {
            //     AWS_S3_BUCKET = 'temp-20250320'
            // }
            steps {
                withCredentials([usernamePassword(credentialsId: 'my-s3-key', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) 
                {   
                    sh '''
                        aws --version
                        aws s3 ls
                        echo "Hello S3!" > index.html
                        aws s3 cp index.html s3://my-bucket-20250125/index.html
                        # aws s3 sync build s3://$AWS_S3_BUCKET
                    '''
                }
            }
        }
    }
}