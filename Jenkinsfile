pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
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
            echo 'Build Successful'
        }

        failure {
            emailext(
                subject: "Build Failed",
                body: "Please check the Jenkins build.",
                recipientProviders: [developers()]
            )
        }

    }
}