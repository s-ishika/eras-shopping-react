pipeline {
    agent any

    tools {
        // This must match the exact name you configured in Jenkins Tools
        nodejs 'node' 
    }

    environment {
        // Ensures 'npm test' runs in non-interactive mode without hanging
        CI = 'true' 
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Pulls the latest code from your repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing packages...'
                // Restores exact dependencies using package-lock.json
                sh 'npm ci' 
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running unit tests...'
                sh 'npm test'
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building React application for production...'
                sh 'npm run build'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline has completed execution.'
        }
        success {
            echo 'Build compiled successfully! The static files are in the /build or /dist directory.'
        }
        failure {
            echo 'Pipeline failed. Check the console logs above.'
        }
    }
}