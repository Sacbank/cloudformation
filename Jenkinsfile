pipeline {
    agent any
    stages {
        stage('Create S3 Bucket') {
            steps {
                script {
                    withAWS(region:'us-east-1', credentials:'aws-access-key-id-1') {
                        sh "aws cloudformation create-stack --stack-name EC2-CFT --template-body file://ec2-instance.yml --region 'us-east-1'"
                        sh "aws cloudformation create-stack --stack-name Network-CFT --template-body file://network.yml --region 'us-east-1'"
                    }
                }
            }
        }
        stage('Create EC2 Instance') {
            steps {
                script {
                    withAWS(region:'us-east-1', credentials:'aws-access-key-id-2') {
                         sh "aws cloudformation create-stack --stack-name s3-bucket-CFT --template-body file://s3-bucket.yml --region 'us-east-1'"
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
