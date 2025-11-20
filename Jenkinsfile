pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = "ap-south-1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
            }
        }

        stage('Install Node & Angular CLI') {
            steps {
                sh '''
                    npm install -g @angular/cli
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    npm install
                '''
            }
        }

        stage('Build Angular App') {
            steps {
                sh '''
                    ng build --configuration production
                '''
            }
        }

        stage('Upload to S3 Bucket') {
            steps {
                withAWS(credentials: 'aws-creds') {
                    sh '''
                        aws s3 sync dist/YOUR_PROJECT_NAME s3://
hariprasadmanigandla/ --delete
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "🎉 Deployment Completed Successfully!"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}
