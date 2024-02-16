pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Clone the repository
                    checkout scm
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build steps (replace with your build commands)
                    sh 'echo "Building..."'
                    sh 'ls'
                }
            }
        }
        
    }
}
