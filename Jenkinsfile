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
                    emailext attachLog: true, body: 'Unit and Integration Test Success. Logs attached.', subject: 'Unit and Integration Test Success', to: 'Gurparsaad2003@gmail.com'
                }
                failure {
                    emailext attachLog: true, body: 'Unit and Integration Test Failure. Logs attached.', subject: 'Unit and Integration Test Failure', to: 'Gurparsaad2003@gmail.com'
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
                    emailext attachLog: true, body: "Security Scan passed. Logs attached.", subject: "Security Scan Success", to: "Gurparsaad2003@gmail.com"
                }
                failure {
                    emailext attachLog: true, body: "Security Scan failed. Logs attached.", subject: "Security Scan Failure", to: "Gurparsaad2003@gmail.com"
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
                    emailext attachLog: true, body: "Integration Tests on Staging passed. Logs attached.", subject: "Integration Tests on Staging Success", to: "Gurparsaad2003@gmail.com"
                }
                failure {
                    emailext attachLog: true, body: "Integration Tests on Staging failed. Logs attached.", subject: "Integration Tests on Staging Failed", to: "Gurparsaad2003@gmail.com"
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
