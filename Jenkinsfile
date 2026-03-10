pipeline {
    agent any

    environment {
        IMAGE_NAME = "rileymo97/product-service"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test --if-present'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                sh 'docker scout cves ${IMAGE_NAME}:latest || true'
            }
        }

        stage('Container Build') {
            steps {
                echo "Building Docker image ${IMAGE_NAME}:${IMAGE_TAG}..."
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Container Push') {
            when {
                anyOf {
                    branch 'main'
                    branch 'develop'
                }
            }
            steps {
                echo 'Pushing image to Docker Hub...'
                sh 'docker push ${IMAGE_NAME}:${IMAGE_TAG}'
                sh 'docker push ${IMAGE_NAME}:latest'
            }
        }

        stage('Deploy') {
            when {
                anyOf {
                    branch 'main'
                    branch 'develop'
                }
            }
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        echo 'Deploying to Production...'
                    } else if (env.BRANCH_NAME == 'develop') {
                        echo 'Deploying to Dev...'
                    } else if (env.BRANCH_NAME.startsWith('release/')) {
                        echo 'Deploying to Staging...'
                    }
                }
            }
        }

    }

    post {
        success {
            echo "Pipeline succeeded! Image: ${IMAGE_NAME}:${IMAGE_TAG}"
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}