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
        stage("Prepare") {
            steps {
                script {
                    sh 'npm install --force'
                }
            }
        }

        stage("Build") {
            steps {
                script {
                    sh 'npm run build'
                    sh 'mv build dist'
                }
            }
        }

        stage("Deploy") {
            steps {
                script {
                    sh 'aws s3 cp dist s3://test-websitehosting-2/ --recursive'
                }
            }
        }
    }
}

