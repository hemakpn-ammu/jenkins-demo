pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building project'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
            }
        }

    }

    post {

        success {
            script {
                def developerEmail = sh(
                    script: "git log -1 --pretty=format:%ae",
                    returnStdout: true
                ).trim()

                emailext(
                    subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """
Hello,

Your commit build completed successfully.

Job: ${env.JOB_NAME}
Build: ${env.BUILD_NUMBER}
URL: ${env.BUILD_URL}
""",
                    to: developerEmail
                )
            }
        }

        failure {
            script {
                def developerEmail = sh(
                    script: "git log -1 --pretty=format:%ae",
                    returnStdout: true
                ).trim()

                echo "Sending email to: ${developerEmail}"

                emailext(
                    subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """
Hello,

Your commit caused the Jenkins build failure.

Job: ${env.JOB_NAME}
Build: ${env.BUILD_NUMBER}
URL: ${env.BUILD_URL}

Please check the Jenkins console output.
""",
                    to: developerEmail
                )
            }
        }

    }
}
