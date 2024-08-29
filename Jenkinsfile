pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo "Building ..."
                echo "mvn clean package"
            }
        }
        stage("Unit and Integration Test"){
            steps{
                echo "Testing ..."
                echo "mvn test"
            }
            post{
                always{
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Unit and Integration Test Status Email",
                    body: "Unit and Integration Test log attached!"
                }
            }
        }
        stage("Code Analysis"){
            steps{
                echo "Analysing ..."
                echo "mvn sonar:sonar"
            }
        }
        stage("Security Scan"){
            steps{
                echo "Scanning ..."
                echo "mvn org.owasp:dependency-check-maven:check"
            }
            post{
                always{
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Security Scan Status Email",
                    body: "Security Scan log attached!"
                }
            }
        }
        stage("Deploy and Staging"){
            steps{
                echo "Deploying ..."
                echo "aws deploy create-deployment"
            }
        }
        stage("Integration Tests on Staging"){
            steps{
                echo "Testing on Staging ..."
                echo "mvn verify"
            }
            post{
                always{
                    mail to: "Gurparsaad2003@gmail.com",
                    subject: "Integration Tests on Staging Status Email",
                    body: "Integratinon Tests on Staging log attached!"
                }
            }
        }
        stage("Deploy to Production"){
            steps{
                echo "Deploying to production ..."
                echo "aws deploy create-deployment"
            }
        }
    }
}
