pipeline {
    environment {
        AWS_ACCESS_KEY_ID_1 = credentials('aws-access-key-id-1') // Credentials for AWS account 1
        AWS_SECRET_ACCESS_KEY_1 = credentials('aws-secret-access-key-1')
        // AWS_ACCESS_KEY_ID_2 = credentials('aws-access-key-id-2') // Credentials for AWS account 2
        // AWS_SECRET_ACCESS_KEY_2 = credentials('aws-secret-access-key-2')
    }
    agent any
    stages {
        stage('Create S3 Bucket') {
            steps {
                script {
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID_1', credentialsId: 'aws-access-key-id-1', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY_1']]) {
                        sh "aws cloudformation create-stack --stack-name s3bucketcft --template-body file://s3-bucket.yml --region 'us-east-1'"
                    }
                }
            }
        }
        
    //     stage('Create EC2 Instance') {
    //         steps {
    //             script {
    //                 withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID_2', credentialsId: 'aws-access-key-id-2', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY_2']]) {
    //                     sh "aws cloudformation create-stack --stack-name Ec2cft --template-body file://ec2-instance.yml --region 'us-east-1'"
    //                 }
    //             }
    //         }
    //     }
    // }
    post {
        always {
            cleanWs()
        }
    }
}
