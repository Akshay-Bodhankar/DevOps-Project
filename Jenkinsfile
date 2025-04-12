pipeline {
    agent any

    environment {
        APP_ENV = 'development'
    }

    options {
        skipDefaultCheckout true
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "🔁 Checked out code from branch: ${env.BRANCH_NAME}"
            }
        }

        stage('Build') {
            steps {
                echo "🔨 Building the application..."
                sh 'echo Build successful!'
            }
        }

        stage('Test') {
            steps {
                echo "🧪 Running tests..."
                sh 'echo All tests passed!'
            }
        }

        stage('Deploy to Staging') {
            when {
                not {
                    changeRequest()
                }
            }
            steps {
                echo "🚀 Deploying to STAGING from branch: ${env.BRANCH_NAME}"
                // your staging deploy logic here
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                input message: 'Deploy to Production?', ok: 'Yes'
                echo "🚀 Deploying to PRODUCTION from branch: ${env.BRANCH_NAME}"
                // your production deploy logic here
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Please check the logs."
        }
        always {
            echo "🧹 Cleaning workspace..."
            cleanWs()
        }
    }
}
