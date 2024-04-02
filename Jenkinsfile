pipeline {
    agent any
    stages {
        stage('Update Network') {
            steps {
                script {
                    withAWS(region:'us-east-1', credentials:'aws-access-key-id-1') {
                        sh "aws cloudformation update-stack --stack-name Network-CFT --template-body file://network.yml --region 'us-east-1' --no-fail-on-empty-changeset" 
                        echo "Waiting for Network stack to be updated..."
                        sh "aws cloudformation wait stack-update-complete --stack-name Network-CFT --region 'us-east-1'"
                    }
                }
            }
        }
        stage('Update EC2') {
            steps {
                script {
                    withAWS(region:'us-east-1', credentials:'aws-access-key-id-1') {
                        sh "aws cloudformation update-stack --stack-name EC2-CFT --template-body file://ec2-instance.yml --capabilities CAPABILITY_NAMED_IAM --region 'us-east-1' --no-fail-on-empty-changeset"
                    }
                }
            }
        }
        stage('Update s3 Bucket') {
            steps {
                script {
                    withAWS(region:'us-east-1', credentials:'aws-access-key-id-2') {
                        sh "aws cloudformation update-stack --stack-name s3-bucket-CFT --template-body file://s3-bucket.yml --region 'us-east-1' --no-fail-on-empty-changeset"
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
