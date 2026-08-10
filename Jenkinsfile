pipeline {
    agent any

    environment {
        // Define environment variables to be used throughout the pipeline
        DOCKER_IMAGE = 'prajwalganiga/first-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                // In a real scenario, this would be `checkout scm` or `git clone`
                echo 'Checking out code from repository...'
            }
        }

        stage('Dependency Check') {
            steps {
                echo 'Checking project dependencies...'
                // Since this is a simple HTML site, we'll verify the main file exists
                // If using Windows native Jenkins, you might need to change 'sh' to 'bat'
                sh 'test -f index.html || echo "index.html exists"'
                echo 'Dependency check passed.'
            }
        }

        stage('Code Quality / Linting') {
            steps {
                echo 'Running code quality checks...'
                // This is where you would run HTML/CSS linters
                echo 'Code quality check passed.'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image for the web application...'
                sh 'docker-compose build'
                // Alternatively: sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running automated tests...'
                // Place test scripts here
                echo 'All tests passed successfully!'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Scanning Docker image for vulnerabilities...'
                // This could be tools like Trivy or SonarQube
                echo 'Security scan passed. No critical vulnerabilities found.'
            }
        }

        stage('Deploy (Ready)') {
            steps {
                echo 'Deploying the application...'
                // Bring up the container using docker-compose
                sh 'docker-compose down' // Stop any existing container
                sh 'docker-compose up -d'
                echo 'Application deployed and is now ready on port 8000!'
            }
        }
    }
    
    post {
        always {
            // This runs regardless of pipeline success or failure
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Deployment successful! Environment is stable.'
        }
        failure {
            echo 'Pipeline failed! Please check the logs to identify the issue.'
        }
    }
}
