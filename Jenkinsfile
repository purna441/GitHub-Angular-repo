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
                sh '''
                    npm install            
                    npm install @angular/cli --save-dev
                    '''
                   
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
