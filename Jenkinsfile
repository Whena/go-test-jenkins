pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo "Checking out code from Git repository..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building Go application..."
                sh 'go build -o app main.go'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'go test ./... -v'
            }
        }
    }

    post {
        success {
            echo "Build and test completed successfully!"
        }
        failure {
            echo "Build or test failed!"
        }
    }
}
