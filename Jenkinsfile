pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = '${FIREBASE_TOKEN}'
    }

    stages {
        stage('Build') {
            steps {
               	sh 'npm config set prefix "$WORKSPACE/.npm-global"'
		sh 'export PATH="$WORKSPACE/.npm-global/bin:$PATH" && npm install -g firebase-tools'
            }
        }

        stage('Testing Deploy') {
            steps {
                sh 'firebase deploy --only hosting --project final-testing --token=$FIREBASE_TOKEN'
            }
        }

        stage('Staging Deploy') {
            steps {
                sh 'firebase deploy --only hosting --project final-staging --token=$FIREBASE_TOKEN'
            }
        }

        stage('Production Deploy') {
            steps {
                sh 'firebase deploy --only hosting --project final-production --token=$FIREBASE_TOKEN'
            }
        }
    }
}
