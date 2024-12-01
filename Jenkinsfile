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
        go build -o hello-world main.go
        '''
    }
}

        stage('Run') {
    steps {
        echo "Running the Go application..."
        sh '''
        chmod +x hello-world
        ./hello-world
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