pipeline {
    agent any
    stages {
        stage('Create S3 Bucket') {
            steps {
                script {
                    withAWS(region:'us-east-1', credentials:'aws-access-key-id-3') {
                        sh "aws cloudformation create-stack --stack-name s3bucketcft --template-body file://s3-bucket.yml --region 'us-east-1'"
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
