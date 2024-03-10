pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Intentionally misspelled 'g++' as 'gcc++' to cause a compilation error
                    try {
                        sh 'gcc++ -o my_program my_program.cpp'
                        echo 'Build Stage Successful'
                    } catch (Exception e) {
                        echo "Build Failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error 'Build failed'
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Intentionally misspelled './my_program' as './my_program_wrong' to cause a test failure
                    try {
                        def output = sh './my_program_wrong', returnStdout: true
                        echo "Test Output: ${output}"
                        echo 'Test Stage Successful'
                    } catch (Exception e) {
                        echo "Test Failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error 'Test failed'
                    }
                }
            }
            post {
                always {
                    script {
                        // Intentionally added a non-existing shell command to cause a post-test error
                        sh 'echo "Additional tests completed"'
                        sh 'this_command_does_not_exist'
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Intentionally using an invalid shell command to simulate deployment failure
                    try {
                        sh 'non_existing_deploy_command'
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
            // Intentionally removing the echo statement to cause a syntax error
            echo 'Pipeline failed'
        }
        success {
            script {
                // Intentionally misspelled 'repositoryUrl' as 'repositoryURL' to cause an error
                def repositoryUrl = sh(script: 'git config --get remote.origin.url', returnStdout: true)
                echo "Repository URL: ${repositoryURL}"
            }
        }
    }
}
