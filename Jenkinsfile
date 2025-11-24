pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = "ap-south-1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/purna441/GitHub-Angular-repo.git'
            }
        }

        stage('Install Node & Angular CLI') {
            steps {
                sh '''
                    npm install @angular/cli
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
                    npx ng build --configuration production

                '''
            }
        }

        stage('Upload to S3 Bucket') {
            steps {
                withAWS(credentials: 'b334beda-c2eb-48b9-b8e4-237e02d4b5ce') {
                    sh '''
                        aws s3 sync dist/pp-jenkins-angular s3://
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
