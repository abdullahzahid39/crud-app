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

        stage('Docker Setup') {
            steps {
                // Set up Docker environment
                sh '''
                docker-compose down || true
                docker-compose build
                '''
            }
        }

        stage('Deploy') {
            steps {
                // Start the application using Docker Compose
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        always {
            // Clean up Docker containers
            sh 'docker-compose down'
        }
    }
}
