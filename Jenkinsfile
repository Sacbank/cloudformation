pipeline {
    environment {
        AWS_ACCESS_KEY_ID_1 = credentials('aws-access-key-id-1') // Credentials for AWS account 1
        AWS_SECRET_ACCESS_KEY_1 = credentials('aws-secret-access-key-1')
    }
    agent any
    stages {
        stage('Create S3 Bucket') {
            steps {
                script {
                    withAWS(region:'us-east-1', credentials:'aws-access-key-id-1') {
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
