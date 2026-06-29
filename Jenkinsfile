pipeline {
    agent any

    environment {
        DB_USER          = credentials('DB_USER')
        DB_PASSWORD      = credentials('DB_PASSWORD')
        DB_NAME          = credentials('DB_NAME')
        DB_HOST          = credentials('DB_HOST')
        JWT_SECRET       = credentials('JWT_SECRET')
        INIT_ADMIN_EMAIL = credentials('INIT_ADMIN_EMAIL')
    }

    options {
        timestamps()
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Prepare Environment') {
            steps {
                sh '''
                    set -e

                    echo "Creating .env file..."

                    cat > .env <<EOF
                        DB_USER=$DB_USER
                        DB_PASSWORD=$DB_PASSWORD
                        DB_NAME=$DB_NAME
                        DB_HOST=$DB_HOST
                        JWT_SECRET=$JWT_SECRET
                        INIT_ADMIN_EMAIL=$INIT_ADMIN_EMAIL
                        EOF
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    set -e
                    echo "Building Docker images..."
                    docker compose build
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    set -e

                    echo "Stopping old stack..."
                    docker compose down --remove-orphans

                    echo "Starting new stack..."
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    echo "Running container status check..."
                    docker compose ps
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                    echo "Waiting for services to stabilize..."
                    sleep 10

                    echo "Checking API health..."
                    curl -f http://localhost/api/health || exit 1
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment successful 🚀"
        }

        failure {
            echo "Deployment failed ❌ - check logs"
        }
    }
}