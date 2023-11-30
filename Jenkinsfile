pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET_NAME = 'test-websitehosting-2'
        CLOUDFRONT_DISTRIBUTION_ID = 'https://d3b8by6cb086w8.cloudfront.net'
    }

    stages {

        stage('Build and Deploy') {
            steps {
                script {
                    withAWS(credentials: "aws-creds", region: "us-east-1") {
                        // Assume index.html is in the root of your project
                        sh 'aws s3 cp index.html s3://${S3_BUCKET_NAME}/index.html --acl public-read'

                        // Create a CloudFront invalidation for the entire distribution
                        sh "aws cloudfront create-invalidation --distribution-id ${CLOUDFRONT_DISTRIBUTION_ID} --paths '/*'"
                    }
                }
            }
        }
    }
}
