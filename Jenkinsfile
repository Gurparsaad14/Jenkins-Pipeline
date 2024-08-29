pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                echo "Building ..."
                echo 'mvn clean package' 
            }
        }
        stage("Unit and Integration Test") {
            steps {
                echo "Testing ..."
                echo 'mvn test' 
            }
            post {
                success {
                    emailext attachLog: true, body: "Unit and Integration Test failed. Logs attached.", subject: "Unit and Integration Test Failure", to: "Gurparsaad2003@gmail.com",
                }
                failure {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Unit and Integration Test Failure",
                    body: "Unit and Integration Test failed. Logs attached.",
                    attachLog: true
                }
            }
        }
        stage("Code Analysis") {
            steps {
                echo "Analysing ..."
                echo 'sonarqube-scanner' 
            }
        }
        stage("Security Scan") {
            steps {
                echo "Scanning ..."
                echo 'dependency-check' 
            }
            post {
                success {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Security Scan Success",
                    body: "Security Scan passed. Logs attached.",
                    attachLog: true
                }
                failure {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Security Scan Failure",
                    body: "Security Scan failed. Logs attached.",
                    attachLog: true
                }
            }
        }
        stage("Deploy and Staging") {
            steps {
                echo "Deploying ..."
                echo 'aws deploy create-deployment' 
            }
        }
        stage("Integration Tests on Staging") {
            steps {
                echo "Testing on Staging ..."
                echo 'selenium-test-command' 
            }
            post {
                success {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Integration Tests on Staging Success",
                    body: "Integration Tests on Staging passed. Logs attached.",
                    attachLog: true
                }
                failure {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Integration Tests on Staging Failure",
                    body: "Integration Tests on Staging failed. Logs attached.",
                    attachLog: true
                }
            }
        }
        stage("Deploy to Production") {
            steps {
                echo "Deploying to production ..."
                echo 'aws deploy create-deployment'
            }
        }
    }
}
