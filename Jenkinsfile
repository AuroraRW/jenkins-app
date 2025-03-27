pipeline {
    agent any
    environment{
        AWS_DEFAULT_REGION = 'us-east-2'
    }
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
        stage('Deploy to AWS') {
            agent {
                docker {
                    image 'amazon/aws-cli'
                    reuseNode true
                    args '-u root --entrypoint=""'
                }
            }
            
            steps {
                withCredentials([usernamePassword(credentialsId: 'my-s3-key', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) 
                {   
                    sh '''
                        aws --version
                        yum install jq -y
                        
                        LATEST_TD_REVISION=$(aws ecs register-task-definition --cli-input-json file://aws/task-definition.json | jq '.taskDefinition.revision')
                        aws ecs update-service --cluster my-new-Cluster-Prod --service my-new-Service-Prod --task-definition my-new-TaskDefinition-Prod:$LATEST_TD_REVISION
                    '''
                }
            }
        }
    }
}