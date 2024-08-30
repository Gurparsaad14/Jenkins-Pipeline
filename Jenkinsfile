pipeline {
    agent any

    environment {
        // Define a variable to store the email recipient
        RECIPIENT = "Gurparsaad2003@gmail.com"
    }

    stages {
        stage('Build') {
            steps {
                // Use Maven to build the code
                echo 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                // Capture the logs
                script {
                    try {
                        echo 'mvn test'
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
            post {
                always {
                    // Send an email with the test logs attached
                    emailext attachLog: true,
                             attachmentsPattern: 'test.log',
                             body: "Unit and Integration Tests ${currentBuild.result}: Please find the attached logs.",
                             subject: "Unit and Integration Tests ${currentBuild.result}",
                             to: "${RECIPIENT}"
                }
            }
        }

        stage('Code Analysis') {
            steps {
                // Integrate a code analysis tool like SonarQube
                echo 'sonar-scanner'
            }
        }

        stage('Security Scan') {
            steps {
                // Capture the logs
                script {
                    try {
                        echo 'OWASP Security Scan'
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
            post {
                always {
                    // Send an email with the security scan logs attached
                    emailext attachLog: true,
                             attachmentsPattern: 'security_scan.log',
                             body: "Security Scan ${currentBuild.result}: Please find the attached logs.",
                             subject: "Security Scan ${currentBuild.result}",
                             to: "${RECIPIENT}"
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                // Deploy the application to a staging server
                echo 'aws deploy create-deployment'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on the staging environment
                echo 'mvn integration-test'
            }
        }

        stage('Deploy to Production') {
            steps {
                // Deploy the application to a production server
                echo 'aws deploy create-deployment'
            }
        }
    }

    post {
        success {
            // Send notification email on overall pipeline success
            emailext body: "Pipeline passed successfully.",
                     subject: "Pipeline Passed",
                     to: "${RECIPIENT}"
        }
        failure {
            // Send notification email on overall pipeline failure
            emailext body: "Pipeline failed.",
                     subject: "Pipeline Failed",
                     to: "${RECIPIENT}"
        }
    }
}
