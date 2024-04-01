pipeline {
    agent any
    
    parameters {
        string(name: 'StackName', defaultValue: 'MyStack', description: 'Name of the CloudFormation stack')
        string(name: 'Region', defaultValue: 'us-east-1', description: 'AWS region to deploy the stack')
        string(name: 'Template1', defaultValue: 'D:\CFT\s3-bucket.yml', description: 'cloudformation template')
        string(name: 'Template2', defaultValue: 'D:\CFT\EC2-ubuntu2204-instance.yml', description: 'cloudformation template')
    }
    
    stages {
        stage('Deploy Stack') {
            steps {
                script {
                    def awsCliCmd = "aws cloudformation deploy --region ${params.Region} --stack-name ${params.StackName} --template-file ${params.Template1} --capabilities CAPABILITY_IAM"
                    sh awsCliCmd
                    awsCliCmd = "aws cloudformation deploy --region ${params.Region} --stack-name ${params.StackName} --template-file ${params.Template2} --capabilities CAPABILITY_IAM"
                    sh awsCliCmd
                }
            }
        }
    }
    
    post {
        success {
            echo "Stack deployment successful"
        }
        failure {
            echo "Stack deployment failed"
        }
    }
}
