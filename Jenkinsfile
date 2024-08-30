pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                echo "Building ..."
                bat 'mvn clean package' 
            }
        }
        stage("Unit and Integration Test") {
            steps {
                echo "Running Unit and Integration Tests ..."
                bat 'mvn test' 
            }
            post {
                success {
                    emailext attachLog: true, body: "Unit and Integration Test Success. Logs attached.", subject: "Unit and Integration Test Success", to: "Gurparsaad2003@gmail.com"
                }
                failure {
                    emailext attachLog: true, body: "Unit and Integration Test failed. Logs attached.", subject: "Unit and Integration Test Failure", to: "Gurparsaad2003@gmail.com"
                }
            }
        }
        stage("Code Analysis") {
            steps {
                echo "Running Code Analysis ..."
                bat 'sonar-scanner' 
            }
        }
        stage("Security Scan") {
            steps {
                echo "Running Security Scan ..."
                bat 'dependency-check.bat' 
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
                echo "Deploying to Staging ..."
                bat 'aws deploy create-deployment --application-name <app-name> --deployment-group-name <group-name> --s3-location <s3-bucket>'
            }
        }
        stage("Integration Tests on Staging") {
            steps {
                echo "Running Integration Tests on Staging ..."
                bat 'selenium-test-command' 
            }
            post {
                success {
                    emailext attachLog: true, body: "Integration Tests on Staging passed. Logs attached.", subject: "Integration Tests on Staging Success", to: "Gurparsaad2003@gmail.com"
                }
                failure {
                    emailext attachLog: true, body: "Integration Tests on Staging failed. Logs attached.", subject: "Integration Tests on Staging Failure", to: "Gurparsaad2003@gmail.com"
                }
            }
        }
        stage("Deploy to Production") {
            steps {
                echo "Deploying to Production ..."
                bat 'aws deploy create-deployment --application-name <app-name> --deployment-group-name <group-name> --s3-location <s3-bucket>'
            }
        }
    }
}
