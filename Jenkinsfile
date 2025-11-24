pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/purna441/GitHub-Angular-repo.git'
            }
        }

        stage('Install Node & Angular CLI') {
            steps {
                sh '''
                    npm install
                    npm install @angular/cli --save-dev
                '''
            }
        }

        stage('Build Angular App') {
            steps {
                sh 'ng build --configuration production'
            }
        }

        stage('Upload to S3') {
            steps {
                withAWS(credentials: 'b334beda-c2eb-48b9-b8e4-237e02d4b5ce', region: 'ap-south-1') {
                    s3Upload bucket: 'pp-jenkins-angular',
                            includePathPattern: 'dist/**/*',
                            workingDir: 'dist/my-angular-app'
                }
            }
        }

    }
}
