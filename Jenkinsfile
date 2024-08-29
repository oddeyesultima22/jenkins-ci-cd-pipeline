pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Use a build automation tool, e.g., Maven
                bat 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Use a test automation tool, e.g., JUnit
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code...'
                // Use a code analysis tool, e.g., SonarQube
                bat 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Use a security scanning tool, e.g., OWASP Dependency Check
                bat 'dependency-check.bat --scan .'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Deploy to a staging server, e.g., using SCP or other tools
                bat 'scp target\\my-app.jar user@staging-server:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Run tests in the staging environment
                bat 'ssh user@staging-server "cd /path/to/deploy && ./run-tests.sh"'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Deploy to a production server
                bat 'scp target\\my-app.jar user@production-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            emailext to: 'aggarwalutkarsh989@gmail.com',
                     subject: "Pipeline Successful: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                     body: "Good news, the pipeline succeeded!"
        }
        failure {
            emailext to: 'aggarwalutkarsh989@gmail.com',
                     subject: "Pipeline Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                     body: "Something went wrong. Please check the logs."
        }
    }
}
