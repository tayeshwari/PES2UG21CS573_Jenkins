pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Compile the .cpp file
                    sh 'g++ -o my_program my_program.cpp'
                    echo 'Build Stage Successful'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Run the compiled program and print its output
                    sh './my_program'
                    echo 'Test Stage Successful'
                }
            }
            post {
                always {
                    script {
                        // Add any additional test steps or checks here if needed
                        echo 'Running additional test steps or checks...'
                        // Example: Run a shell command
                        sh 'echo "Additional tests completed"'
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    try {
                        echo 'Deployment Successful'
                    } catch (Exception e) {
                        echo "Deployment Failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error 'Deployment failed'
                    }
                }
            }
        }
    }
    
    post {
        failure {
            echo 'Pipeline failed'
        }
        success {
            script {
                // Print the repository URL
                def repositoryUrl = sh(script: 'git config --get remote.origin.url', returnStdout: true).trim()
                echo "Repository URL: ${repositoryUrl}"
            }
        }
    }
}
