pipeline {
             agent any
    stages {
        stage('Parallel dynamic agents') {
            parallel {
                stage('Build (Python)') {
                    agent {
                        docker {
                            image 'python:3.11-slim'
                            label 'docker-agent'
                            args  '-u root'
                            reuseNode true
                        }
                    }
                    steps {
                        sh 'hostname'
                        sh 'python3 --version'
                        sh 'pip install --quiet pytest && pytest --version'
                    }
                }
                stage('Tools (Node)') {
                    agent {
                        docker {
                            image 'node:20-slim'
                            label 'docker-agent'
                            args  '-u root'
                            reuseNode true
                        }
                    }
                    steps {
                        sh 'hostname'
                        sh 'node --version'
                        sh 'npm --version'
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Build #${env.BUILD_NUMBER} finished — agents have been destroyed."
        }
    }
}
