pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-credentials',
                    url: 'https://github.com/purna441/GitHub-Angular-repo.git'
            }
        }

        stage('Install Node & Angular CLI') {
            steps {
                sh 'npm install -g @angular/cli'
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('AngularApp') {
                    sh 'npm install'
                }
            }
        }

        stage('Build Angular App') {
            steps {
                dir('AngularApp') {
                    sh 'npx ng build --configuration production'
                }
            }
        }

        stage('Upload to S3 Bucket') {
            steps {
                sh '''
                aws s3 sync AngularApp/dist/angular-app-name s3://pp-jenkins-angular/ --delete
                '''
            }
        }
    }
}
