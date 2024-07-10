pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS 14' // Ensure you have a Node.js tool configured in Jenkins
        PATH = "${env.NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git 'https://github.com/WaailRajpoot/crud-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Run tests (if any)
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                // Build the application (if needed)
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Start the application
                sh 'npm start &'
            }
        }
    }

    post {
        always {
            script {
                // Wrap the cleanup in a node block
                node {
                    // Ensure the port is free before running the app again using lsof
                    sh 'lsof -t -i tcp:3000 | xargs kill -9 || true'
                }
            }
        }
    }
}
