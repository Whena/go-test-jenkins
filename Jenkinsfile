pipeline {
    agent any

    environment {
        APP_BINARY = 'hello-world'                   // Nama binary hasil build
        REMOTE_USER = 'service'                      // User server target
        REMOTE_HOST = '157.10.160.194'               // IP server target
        TARGET_DIR = '/var/www/myapp'                // Direktori target di server
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
                go build -o ${APP_BINARY} main.go
                '''
            }
        }

        stage('Run') {
            steps {
                echo "Running the Go application locally..."
                sh '''
                chmod +x ${APP_BINARY}
                ./${APP_BINARY}
                '''
            }
        }

        stage('Deploy to Server') {
    steps {
        sshagent(['5db0495e-c861-47b7-8bb4-f2c1b451c676']) { // ID credentials SSH di Jenkins
            sh '''
            echo "Creating target directory if not exists..."
            ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} "mkdir -p ${TARGET_DIR}"

            echo "Copying binary to remote server..."
            scp -o StrictHostKeyChecking=no ${APP_BINARY} ${REMOTE_USER}@${REMOTE_HOST}:${TARGET_DIR}/

            echo "Running binary on remote server..."
            ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST} "
            chmod +x ${TARGET_DIR}/${APP_BINARY}
            ${TARGET_DIR}/${APP_BINARY}
            "
            '''
        }
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
