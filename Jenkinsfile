pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1 : Build'
                echo 'Task: Compile and package the code.'
                echo 'Tool: Maven, Gradle'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage: Unit and Integration Tests'
                echo 'Task: Run unit and integration tests.'
                echo 'Tool: JUnit, TestNG'
            }
            post {
                always {
                    emailext to: 's223739207@deakin.edu.au',
                        subject: "Unit and Integration Tests Results: ${currentBuild.fullDisplayName}",
                        body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.result}. Check the attached logs for more details.",
                        attachLog: true
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage: Code Analysis'
                echo 'Task: Analyze the code for quality and standards.'
                echo 'Tool: SonarQube, Checkstyle'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage: Security Scan'
                echo 'Task: Perform a security scan to identify vulnerabilities.'
                echo 'Tool: OWASP Dependency-Check, Checkmarx'
            }
            post {
                always {
                    emailext to: 's223739207@deakin.edu.au',
                        subject: "Security Scan Results: ${currentBuild.fullDisplayName}",
                        body: "The Security Scan stage has completed with status: ${currentBuild.result}. Check the attached logs for more details.",
                        attachLog: true
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage: Deploy to Staging'
                echo 'Task: Deploy the application to a staging environment.'
                echo 'Tool: AWS CLI, Ansible'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage: Integration Tests on Staging'
                echo 'Task: Run integration tests on the staging environment.'
                echo 'Tool: Selenium, Postman'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage: Deploy to Production'
                echo 'Task: Deploy the application to a production environment.'
                echo 'Tool: AWS Elastic Beanstalk, Kubernetes'
            }
        }
    }

    post {
        always {
            emailext to: 's223739207@deakin.edu.au',
                subject: "Pipeline ${currentBuild.fullDisplayName} Results",
                body: "Pipeline completed. Result: ${currentBuild.result}. Check Jenkins for details.",
                attachLog: true
        }
    }
}
