pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building ...'
                // Add your build steps here
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests ...'
                // Add your test steps here
            }
            post {
                always {
                    script {
                        def testLog = currentBuild.rawBuild.getLog(1000).join("\n")
                        writeFile file: 'test-log.txt', text: testLog
                    }
                    mail(
                        to: 'your-email@example.com',
                        subject: "Jenkins Test Stage: ${currentBuild.currentResult}",
                        body: "The Test stage has completed with status: ${currentBuild.currentResult}. Please find the logs attached.",
                        attachLog: true,
                        attachmentsPattern: 'test-log.txt'
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code ...'
                // Add your code analysis steps here
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan ...'
                // Add your security scan steps here
            }
            post {
                always {
                    script {
                        def securityLog = currentBuild.rawBuild.getLog(1000).join("\n")
                        writeFile file: 'security-log.txt', text: securityLog
                    }
                    mail(
                        to: 'your-email@example.com',
                        subject: "Jenkins Security Scan Stage: ${currentBuild.currentResult}",
                        body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}. Please find the logs attached.",
                        attachLog: true,
                        attachmentsPattern: 'security-log.txt'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging ...'
                // Add your deployment steps here
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging ...'
                // Add your integration test steps here
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production ...'
                // Add your deployment steps here
            }
        }
    }
}
