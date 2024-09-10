pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                echo "Building ..."
                echo "mvn clean package"
            }
        }
        stage("Unit and Integration Test") {
            steps {
                echo "Testing ..."
                echo "JUnit and TestNG Testing ..."
            }
            post {
                success {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Unit and Integration Test Passed",
                    body: "Unit and Integration Test passed successfully. Check the logs for more details.",
                }
                failure {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Unit and Integration Test Failed",
                    body: "Unit and Integration Test failed. Check the logs for more details.",
                }
            }
        }
        stage("Code Analysis") {
            steps {
                echo "Analysing ..."
                echo "mvn sonar:sonar"
                echo "sonarqube code analysis"
            }
        }
        stage("Security Scan") {
            steps {
                echo "Scanning ..."
                echo "owasp dependency-check"
            }
            post {
                success {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Security Scan Passed",
                    body: "Security Scan passed successfully. Check the logs for more details.",
                }
                failure {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Security Scan Failed",
                    body: "Security Scan failed. Check the logs for more details.",
                }
            }
        }
        stage("Deploy and Staging") {
            steps {
                echo "Deploying ..."
                echo "aws deploy create-deployment"
            }
        }
        stage("Integration Tests on Staging") {
            steps {
                echo "Testing on Staging ..."
                echo "Selenium Testing ..."
            }
            post {
                success {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Integration Tests on Staging Passed",
                    body: "Integration Tests on Staging passed successfully. Check the logs for more details.",
                }
                failure {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Integration Tests on Staging Failed",
                    body: "Integration Tests on Staging failed. Check the logs for more details.",
                }
            }
        }
        stage("Deploy to Production") {
            steps {
                echo "Deploying to production ..."
                echo "aws deploy create-deployment"
            }
        }
    }
}
