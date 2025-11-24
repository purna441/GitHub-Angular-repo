pipeline {
    agent any

    stages {

        stage('Install Node & Angular CLI') {
            steps {
                sh 'curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -'
                sh 'sudo apt-get install -y nodejs'
                sh 'npm install -g @angular/cli'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Angular App') {
            steps {
                sh 'ng build --configuration production'
            }
        }

        stage('Upload to S3 Bucket') {
            steps {
                sh 'aws s3 sync dist/ s3://pp-jenkins-angular --delete'
            }
        }
    }

    post {
        failure {
            echo "❌ Deployment Failed!"
        }
        success {
            echo "✅ Deployment Successful!"
        }
    }
}
