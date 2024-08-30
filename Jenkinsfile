pipeline {
    agent {
        docker {
            image 'maven:3.8.1-jdk-11'
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Code building with Maven'
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with Maven'
                sh 'mvn test'
            }
            post {
                success {
                    echo 'Tests passed!'
                }
                failure {
                    echo 'Tests failed!'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Code analysis with SonarQube'
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Security scan with Maven. Runs an OWASP Dependency check'
                sh 'mvn dependency-check:check'
            }
            post {
                always {
                    emailext to: 's223739207@deakin.edu.au',
                        subject: "Security Scan Results: ${currentBuild.fullDisplayName}",
                        body: "Security scan stage ${currentBuild.result}.",
                        attachLog: true,
                        attachmentsPattern: '**/dependency-check-report.html'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment'
                sh './deploy-to-staging.sh'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment'
                sh './run-staging-tests.sh'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment'
                sh './deploy-to-production.sh'
            }
        }
    }

    post {
        always {
            emailext to: 's223739207@deakin.edu.au',
                 subject: "Pipeline ${currentBuild.fullDisplayName} Results",
                 body: "Pipeline completed. Result: ${currentBuild.result}. Check Jenkins for details.",
                 attachLog: true,
                 attachmentsPattern: '**/build.log'
        }
    }
}
