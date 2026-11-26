
pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "abh-app"
        DOCKER = "C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe"
        PYTHON = "C:\\Users\\STUDENT\\AppData\\Local\\Programs\\Python\\Python313\\python.exe"
    }

    stages {

        stage('1. Checkout Code') {
            steps {
                checkout scm
                echo 'GitHub source code downloaded successfully!'
            }
        }

        stage('2. Application Build & Test') {
            steps {
                echo 'Running Python application...'

                bat '"%PYTHON%" app.py'

                echo 'Application executed successfully!'
            }
        }

        stage('3. Check Docker') {
            steps {
                echo 'Checking Docker installation...'

                bat '"%DOCKER%" --version'

                bat '"%DOCKER%" info'
            }
        }

        stage('4. Build & Tag Docker Image') {
            steps {
                echo 'Building Docker image...'

                bat '"%DOCKER%" build -t localhost:5000/abh-app:%BUILD_NUMBER% -t localhost:5000/abh-app:latest .'
            }
        }

        stage('5. Push Image to Registry') {
            steps {
                echo 'Pushing Docker image to local registry...'

                bat '"%DOCKER%" push localhost:5000/abh-app:%BUILD_NUMBER%'

                bat '"%DOCKER%" push localhost:5000/abh-app:latest'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS! Jenkins pipeline completed successfully.'
            echo 'Docker image pushed to localhost:5000/abh-app'
        }

        failure {
            echo 'BUILD FAILED! Please check the Console Output.'
        }

        always {
            echo 'Jenkins pipeline execution finished.'
        }
    }
}
