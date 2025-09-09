pipeline {
    agent { label 'build-heavy' }
    stages {
        stage('Build Front') {
            steps {
                echo "Build front..."
            }
            stage('Checkout') {
                steps {
                    checkout scm
                }
            }
            stage('Install Dependencies') {
                steps {
                    sh 'npm install'
                }
            }
            stage('Build') {
                steps {
                    sh 'npm run build'
                }
            }
        }
    }
}
