pipeline {
    agent any

    environment {
        NODE_HOME = '/usr/local/bin' // Path to Node.js
        PATH = "$NODE_HOME:$PATH"
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

        stage('Run Tests') {
            steps {
                // Run tests
                sh 'npm test'
            }
        }

        stage('Start Application') {
            steps {
                // Start the application
                sh 'npm start'
            }
        }
    }

    post {
        always {
            // Clean up workspace after the pipeline run
            cleanWs()
        }
    }
}
