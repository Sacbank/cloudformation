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
        stage('Create EC2 Instance') {
            steps {
                script {
                    withAWS(region:'us-east-1', credentials:'aws-access-key-id-4') {
                        sh "aws cloudformation create-stack --stack-name Ec2cft --template-body file://ec2-instance.yml --region 'us-east-1'"
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
