pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo " Build - Build the code using a build automation tool for stage 1(e.g., Maven)."
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo " Unit and Integration Tests - Run unit tests to ensure the code functions as expected and run integration tests to ensure the different components of the application work together as expected for stage 2."
            }
        }
        stage('Code Analysis') {
            steps {
                echo " Code Analysis - Integrate a code analysis tool (e.g., SonarQube) to analyze the code and ensure it meets industry standards for stage 3."
            }
        }
        stage('Security Scan') {
            steps {
                echo " Security Scan - Perform a security scan on the code using a tool to identify any vulnerabilities (e.g., OWASP Dependency-Check) for stage 4."
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo " Deploy to Staging - Deploy the application to a staging server (e.g., AWS EC2 instance) using a deployment tool (e.g., AWS CodeDeploy) for stage 5."
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo " Integration Tests on Staging - Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment for stage 6."
            }
        }
        stage('Deploy to Production') {
            steps {
                echo " Deploy to Production - Deploy the application to a production server (e.g., AWS EC2 instance) using a deployment tool (e.g., AWS CodeDeploy) for stage 7."
            }
        }
    }

    post {
        always {
            script {
                def logFile = 'build.log'
                def logLines = currentBuild.getRawBuild().getLog(1000)
                writeFile file: logFile, text: logLines.join('\n')
            }
            echo 'Pipeline completed.'
        }
        success {
            emailext(
                to: 'choudharijay3@gmail.com',
                subject: "Pipeline Successful: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                body: "Good news, the pipeline succeeded! See attached log for details.",
                attachmentsPattern: 'build.log'
            )
        }
        failure {
            emailext(
                to: 'choudharijay3@gmail.com',
                subject: "Pipeline Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                body: "Something went wrong. Please check the attached logs for more details.",
                attachmentsPattern: 'build.log'
            )
        }
    }
}
