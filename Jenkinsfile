pipeline {
    agent any

    environment {
        RECIPIENT_EMAIL = "namquang.study@gmail.com"
        LOG_FILE_PATH = "logs/build-log.txt"
    }

    stages {
        stage('Build') {
            steps {
                echo "Build the code using 'CMake'"
                //sh 'cmake --build
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Run unit tests to ensure code functionality and integration tests to ensure components work together, then send the status to the email."
                echo "Using Ctest from CMake"
                //sh 'cd build && ctest --output-on-failure'
            }
            post {
                always {
                    script {
                        emailext(
                            subject: "Unit and Integration Tests Stage - ${currentBuild.currentResult}",
                            body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.currentResult}. Please read the attached logs for more details.",
                            to: "${env.RECIPIENT_EMAIL}",
                            attachmentsPattern: "${env.LOG_FILE_PATH}",
                            attachLog: true
                        )
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Task: Perform code analysis to ensure code quality and adherence to industry standards using CppCheck."
                //sh 'cppcheck --enable=all --inconclusive --xml --xml-version=2 . 2> cppcheck.xml'
            }
        }

        stage('Security Scan') {
            steps {
                echo "Perform a security scan to identify vulnerabilities in the c++ code and send the status of the scan to email."
                echo "Using SonarQube for security scanning."
                //sh 'sonar-scanner'
            }
            post {
                always {
                    emailext(
                        subject: "Security Scan Stage - ${currentBuild.currentResult}",
                        body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}. Please read the attached logs for more details.",
                        to: "${env.RECIPIENT_EMAIL}",
                        attachmentsPattern: "${env.LOG_FILE_PATH}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploy the application to a staging server by using SSH to AWS EC2 instance."
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Task: Run integration tests on the staging environment by using CTest or BoostTest."
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Task: Deploy the application to the production environment by using SSH to deploy to AWS EC2 instance."
            }
        }
    }
}
