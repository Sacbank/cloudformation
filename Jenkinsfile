pipeline {
    agent any
    stages {
        stage('Update Network') {
            steps {
                script {
                    try {
                        withAWS(region:'us-east-1', credentials:'aws-access-key-id-1') {
                            sh "aws cloudformation update-stack --stack-name Network-CFT --template-body file://network.yml --region 'us-east-1'"
                            echo "Waiting for Network stack to be updated..."
                            sh "aws cloudformation wait stack-update-complete --stack-name Network-CFT --region 'us-east-1'"
                        }
                    } catch (Exception e) {
                        echo "No updates were needed for Network stack."
                    }
                }
            }
        }
        stage('Update EC2') {
            steps {
                script {
                    try {
                        withAWS(region:'us-east-1', credentials:'aws-access-key-id-1') {
                            sh "aws cloudformation update-stack --stack-name EC2-CFT --template-body file://ec2-instance.yml --capabilities CAPABILITY_NAMED_IAM --region 'us-east-1'"
                        }
                    } catch (Exception e) {
                        echo "No updates were needed for EC2 stack."
                    }
                }
            }
        }
        stage('Update s3 Bucket') {
            steps {
                script {
                    try {
                        withAWS(region:'us-east-1', credentials:'aws-access-key-id-2') {
                            sh "aws cloudformation update-stack --stack-name s3-bucket-CFT --template-body file://s3-bucket.yml --region 'us-east-1'"
                        }
                    } catch (Exception e) {
                        echo "No updates were needed for s3 Bucket stack."
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
