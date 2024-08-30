pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo "Stage 1: Build - Build the code using a build automation tool (e.g., Maven)."
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Stage 2: Unit and Integration Tests - Run unit tests to ensure the code functions as expected and run integration tests to ensure the different components of the application work together as expected."
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Stage 3: Code Analysis - Integrate a code analysis tool (e.g., SonarQube) to analyze the code and ensure it meets industry standards."
            }
        }
        stage('Security Scan') {
            steps {
                echo "Stage 4: Security Scan - Perform a security scan on the code using a tool to identify any vulnerabilities (e.g., OWASP Dependency-Check)."
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Stage 5: Deploy to Staging - Deploy the application to a staging server (e.g., AWS EC2 instance) using a deployment tool (e.g., AWS CodeDeploy)."
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Stage 6: Integration Tests on Staging - Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment."
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Stage 7: Deploy to Production - Deploy the application to a production server (e.g., AWS EC2 instance) using a deployment tool (e.g., AWS CodeDeploy)."
            }
        }
    }

    post {
        always {
            // Archive the console output using a whitelisted method
            script {
                def logFile = 'build.log'
                def logLines = currentBuild.getRawBuild().getLog(1000)
                writeFile file: logFile, text: logLines.join('\n')
            }
            echo 'Pipeline completed.'
        }
        success {
            emailext(
                to: 'aggarwalutkarsh989@gmail.com',
                subject: "Pipeline Successful: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                body: "Good news, the pipeline succeeded! See attached log for details.",
                attachmentsPattern: 'build.log'
            )
        }
        failure {
            emailext(
                to: 'aggarwalutkarsh989@gmail.com',
                subject: "Pipeline Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                body: "Something went wrong. Please check the attached logs for more details.",
                attachmentsPattern: 'build.log'
            )
        }
    }
}
