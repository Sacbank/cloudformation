pipeline {
        environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
    }
    agent any
    stages {
        stage('Submit Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name s3bucketcft --template-body file://s3-bucket.yml --region 'us-east-1'"
            sh "aws cloudformation create-stack --stack-name Ec2cft --template-body file://s3-bucket.yml --region 'us-east-1'"        
              }
             }
            }
            }
