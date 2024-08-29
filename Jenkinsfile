pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                echo "Building ..."
                sh 'mvn clean package' // Assuming you want to run this command
            }
        }
        stage("Unit and Integration Test") {
            steps {
                echo "Testing ..."
                sh 'mvn test' // Assuming JUnit and TestNG are run through Maven
            }
            post {
                success {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Unit and Integration Test Success",
                    body: "Unit and Integration Test passed. Logs attached.",
                    attachLog: true
                }
                failure {
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Unit and Integration Test Failure",
                    body: "Unit and Integration Test failed. Logs attached.",
                    attachLog: false
                }
            }
        }
        stage("Code Analysis") {
            steps {
                echo "Analysing ..."
                sh 'sonarqube-scanner' // Replace with your SonarQube command
            }
        }
        stage("Security Scan") {
            steps {
                echo "Scanning ..."
                sh 'dependency-check' // Replace with your OWASP command
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
                    attachLog: false
                }
            }
        }
        stage("Deploy and Staging") {
            steps {
                echo "Deploying ..."
                sh 'aws deploy create-deployment' // Replace with your AWS deployment command
            }
        }
        stage("Integration Tests on Staging") {
            steps {
                echo "Testing on Staging ..."
                sh 'selenium-test-command' // Replace with your Selenium command
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
                    attachLog: false
                }
            }
        }
        stage("Deploy to Production") {
            steps {
                echo "Deploying to production ..."
                sh 'aws deploy create-deployment' // Replace with your AWS deployment command
            }
        }
    }
}
