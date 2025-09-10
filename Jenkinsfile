pipeline {
    agent any
    parameters {
        choice(name: 'env', choices: ['dev', 'prod'], description: 'Select environment')
    }

    stages {
        stage('Determine Environment') {
            steps {
                script {
                    def targetCluster = ''
                    if (params.env == 'prod') {
                        targetCluster = 'Cluster kube de production'
                    }else if (params.env == 'dev'){
                        targetCluster = 'Cluster kube de dev '
                    }
                    echo "Target Cluster: ${targetCluster}"
                    env.TARGET_CLUSTER = targetCluster
                }
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Tests') {
            steps {
                sh 'npm test -- --ci --reporters=jest-junit'
            }
            post {
                always {
                    junit 'junit.xml'
                }
            }
        }
    }

    post {
        success {
            echo "✅ Frontend build & tests succeeded"
        }
        failure {
            echo "❌ Frontend pipeline failed"
        }
    }
}
