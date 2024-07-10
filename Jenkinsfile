pipeline {
    agent any

    environment {
        NODE_HOME = '/usr/local/bin' // Path to Node.js
        PATH = "$NODE_HOME:$PATH"
    }

    stages {
        stage('Install Node.js') {
            steps {
                // Install Node.js if not already installed
                sh '''
                if ! command -v node &> /dev/null
                then
                    curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
                    sudo apt-get install -y nodejs
                fi
                node -v
                npm -v
                '''
            }
        }

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
                sh 'npm start &'
                // Wait a bit for the app to start
                sleep 5
                // Debug: Check if the application is running
                sh 'curl -I localhost:3000 || true'
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

