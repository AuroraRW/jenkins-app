pipeline {
    agent any
    stages {

        stage("AWS"){
            agent{
                docker{
                    image 'amazon/aws-cli'
                    reuseNode true
                    // args '--entrypoint=""'
                }
            }
            steps{
                withCredentials([usernamePassword(credentialsId: 'my-aws-jenkins', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')])
                 {
                    sh '''
                        --version
                        s3 ls 
                        
                    '''
                }
            }
        }
    }
}