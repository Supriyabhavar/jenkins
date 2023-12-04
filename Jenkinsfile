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
                    // Run Git command to get the current branch
                    def branchName = sh(script: 'git rev-parse --abbrev-ref HEAD', returnStdout: true).trim()
                    
                    // Set the branch name as an environment variable
                    env.BRANCH_NAME = branchName
                    
                    // Print the branch name for verification
                    echo "Branch Name: ${env.BRANCH_NAME}"
                }
                // sh 'echo $BRANCH_NAME'
                // sh 'npm install --force'
            }
        }

        // stage("Build") {
        //     steps {
        //         sh 'npm run build'
        //     }
        // }

        // stage("Deploy") {
        //     steps {
        //         script {
        //             withAWS(credentials: "aws-creds", region: "us-east-1") {
        //                 sh 'ls'
        //                 sh '''
        //                     cd dist/angular-conduit 
        //                     aws s3 cp . s3://${S3_BUCKET_NAME}/ --recursive
        //                 '''
        //             }
        //         }
        //     }
        // }

        // stage("cloudfront-invalidation") {
        //     steps {
        //         script {
        //             withAWS(credentials: "aws-creds", region: "us-east-1") {
        //                 sh "aws cloudfront create-invalidation --distribution-id ${CLOUDFRONT_DISTRIBUTION_ID} --paths '/*'" 
        //             }
        //         }
        //     }
        // }
    }
}
