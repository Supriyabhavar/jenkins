pipeline {
    agent any


   
    parameters {
        string(name: 'S3_BUCKET_NAME', defaultValue: 'test-websitehosting-2', description: 'Enter the S3 bucket name')
    }

    
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET_NAME = 'test-websitehosting-2'
        CLOUDFRONT_DISTRIBUTION_ID = 'E1FENB7LMT5MFJ'
    }

    stages {

        stage('Build and Deploy') {
            steps {
                script {
                    withAWS(credentials: "aws-creds", region: "us-east-1") {
                        // Assume index.html is in the root of your project                        sh 'ls'
                        sh 'aws s3 cp index.html s3://${S3_BUCKET_NAME}/index.html --acl public-read'

                        // Create a CloudFront invalidation for the entire distribution
                        sh "aws cloudfront create-invalidation --distribution-id ${CLOUDFRONT_DISTRIBUTION_ID} --paths '/*'"
                    }
                }
            }
        }
    }
}
