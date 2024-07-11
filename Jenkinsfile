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
                script {
                    // Install pm2 globally if not already installed
                    sh 'npm install -g pm2'

                    // Stop any existing instance of the application managed by pm2
                    sh 'pm2 stop my-app || true' // Don't fail if the process does not exist

                    // Start the application using pm2
                    sh 'pm2 start app.js --name "my-app"'

                    // Save the pm2 process list and corresponding environments
                    sh 'pm2 save'
                }
            }
        }
    }
}
