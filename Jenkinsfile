pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/purna441/GitHub-Angular-repo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('my-angular-app') {
                    sh '''
                        npm install
                        npm install @angular/cli --save-dev
                    '''
                }
            }
        }

        stage('Build Angular App') {
            steps {
                dir('my-angular-app') {
                    sh 'ng build --configuration production'
                }
            }
        }

        stage('Upload to S3') {
            steps {
                dir('my-angular-app/dist/my-angular-app') {
                    withAWS(credentials: 'b334beda-c2eb-48b9-b8e4-237e02d4b5ce', region: 'ap-south-1') {
                        s3Upload bucket: 'pp-jenkins-angular',
                                 includePathPattern: '**/*'
                    }
                }
            }
        }

    }
}
