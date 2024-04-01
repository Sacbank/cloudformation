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
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID_1', credentialsId: 'aws-access-key-id-1', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY_1']]) {
                        sh 'export > exported_variables.txt'
                    }
                }
            }
        }
    }
}
