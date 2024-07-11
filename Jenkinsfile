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
                // Start the application using pm2
                sh 'nohup npm start &'// Install pm2 globally if not already installed
                echo "this is correct"
            }
        }
    }
}
