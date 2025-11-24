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

        stage('Install Dependencies') {
            steps {
                dir('AngularApp') {
                    sh 'npm install'            // installs local node_modules
                    sh 'npm install @angular/cli --save-dev'   // install Angular CLI locally
                    sh './node_modules/.bin/ng build --configuration production'
                   
                }
            }
        }

        stage('Build Angular App') {
            steps {
                dir('AngularApp') {
                    sh 'npm install'sh 'npm install @angular/cli --save-dev'
                    
                    
                }
            }
        }

        stage('Upload to S3 Bucket') {
            steps {
                sh '''
                aws s3 sync AngularApp/dist/angular-app s3://pp-jenkins-angular/ --delete
                '''
            }
        }
    }
}
