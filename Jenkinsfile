pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/yahyaElmjiyed/tp-jenkins-security.git'
            }
        }

        stage('Build') {
            steps {
                echo "Repository cloned successfully"
            }
        }

        stage('Run Tests') {
            steps {
                echo "Simulated test execution"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Simulated security scan"
            }
        }

    }

    post {
        success {
            echo 'Pipeline executed successfully'
        }

        failure {
            echo 'Build failed'
        }
    }
}
