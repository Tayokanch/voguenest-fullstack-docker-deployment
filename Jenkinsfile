pipeline {
    agent any

    environment {
        MONGO_USER      = credentials('MONGO_USER')
        MONGO_PASS      = credentials('MONGO_PASS')
        MONGO_PORT      = credentials('MONGO_PORT')
        JWT_SECRET      = credentials('JWT_SECRET')
        STRIPE_SCRETE = credentials('STRIPE_SECRET')
        MONGO_DB      = credentials('MONGO_DB')
        INIT_ADMIN_EMAIL = credentials('INIT_ADMIN_EMAIL')
        MONGO_URL = credentials('MONGO_URL')
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

                    docker compose up -d --scale voguenest-api=3

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
                    curl -f http://localhost:/api/health || exit 1
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