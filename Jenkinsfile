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
                always {
                    archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive: true
                    mail to: "Gurparsaad2003@gmail.com",
                         subject: "Unit and Integration Test ${currentBuild.currentResult}",
                         body: "Unit and Integration Test ${currentBuild.currentResult}. Logs attached.",
                         attachmentsPattern: '**/target/*.log'
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
                always {
                    archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive: true
                    mail to: "Gurparsaad2003@gmail.com",
                         subject: "Security Scan ${currentBuild.currentResult}",
                         body: "Security Scan ${currentBuild.currentResult}. Logs attached.",
                         attachmentsPattern: '**/target/*.log'
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
                always {
                    archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive: true
                    mail to: "Gurparsaad2003@gmail.com",
                         subject: "Integration Tests on Staging ${currentBuild.currentResult}",
                         body: "Integration Tests on Staging ${currentBuild.currentResult}. Logs attached.",
                         attachmentsPattern: '**/target/*.log'
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
