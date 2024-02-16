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
                    sh 'docker images'
                    sh 'docker build -t theapp .'
                    sh 'docker images'

                    // Run Docker container in the background and capture the container ID
                    def containerId = sh(script: 'docker run -d -p 5000:5000 theapp', returnStdout: true).trim()
                    
                    // Save container ID for later
                    env.CONTAINER_ID = containerId
                }
            }
        }
        stage('Test'){
            steps {
                script {
                    // Wait for a few seconds to ensure the container is fully started
                    sleep time: 10, unit: 'SECONDS'

                    // Run tests using curl against the running container
                    def testOutput = sh(script: 'curl http://34.201.77.43:5000', returnStdout: true).trim()

                    // Check if the output is 'Hello, World!'
                    if (testOutput == 'Hello, World!') {
                        echo 'Test passed: Output is Hello, World!'
                    } else {
                        error 'Test failed: Output is not Hello, World!'
                    }
                }
            }
        } 
        stage('Cleanup') {
            steps {
                script {
                    // Stop and remove the Docker container after tests
                    sh "docker stop ${env.CONTAINER_ID}"
                    sh "docker rm ${env.CONTAINER_ID}"
                }
            }
        }
        
    }
}
