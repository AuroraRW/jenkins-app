pipeline {
    agent any
    stages {

        stage("AWS"){
            agent{
                docker{
                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrypoint=""'
                }
            }
            steps{
                withCredentials([usernamePassword(credentialsId: 'my-aws-jenkins', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')])
                 {
                    sh '''
                        aws --version
                        aws s3 ls 
                        echo "Hello S3!" > index.html
                        aws s3 cp index.html s3://my-new-20250320/index.html
                    '''
                }
            }
        }
        
    }
}