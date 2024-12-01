pipeline {
    agent any

    environment {

        APP_BINARY = 'hello-world'                   // Nama binary hasil build
        REMOTE_USER = 'service'                      // User server target
        REMOTE_HOST = '157.10.160.194'               // IP server target
        TARGET_DIR = '/var/www/myapp'               // Direktori target di server

    }

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
                sh '''
                go mod init example.com/hello || true
                go build -o ${GO_BINARY} main.go
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Running tests (placeholder)..."
                sh '''
                # Jika ada test: go test ./...
                echo "No tests implemented."
                '''
            }
        }

        stage('Run') {
            steps {
                echo "Running the Go application..."
                sh '''
                chmod +x ${GO_BINARY}
                ./${GO_BINARY}
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}