pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'npm config set prefix "$WORKSPACE/.npm-global"'
                sh 'export PATH="$WORKSPACE/.npm-global/bin:$PATH" && npm install -g firebase-tools'
            }
        }

        stage('Testing Deploy') {
            steps {
                withCredentials([file(credentialsId: 'firebase-testing-sa', variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
                    sh 'firebase deploy --only hosting --project final-testing-758ad'
                }
            }
        }

        stage('Staging Deploy') {
            steps {
                withCredentials([file(credentialsId: 'firebase-staging-sa', variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
                    sh 'firebase deploy --only hosting --project final-staging-53d0f'
                }
            }
        }

        stage('Production Deploy') {
            steps {
                withCredentials([file(credentialsId: 'firebase-production-sa', variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
                    sh 'firebase deploy --only hosting --project final-production-eb79a'
                }
            }
        }
    }
}
