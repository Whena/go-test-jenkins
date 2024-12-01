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

 stage('Deploy to Server') {
            steps {
                sshagent(['server-ssh-credentials']) { // ID credentials SSH di Jenkins
                    sh '''
                    echo "Copying binary to remote server..."
                    scp ${APP_BINARY} ${REMOTE_USER}@${REMOTE_HOST}:${TARGET_DIR}/

                    echo "Running binary on remote server..."
                    ssh ${REMOTE_USER}@${REMOTE_HOST} '
                    chmod +x ${TARGET_DIR}/${APP_BINARY}
                    ${TARGET_DIR}/${APP_BINARY}
                    '
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
