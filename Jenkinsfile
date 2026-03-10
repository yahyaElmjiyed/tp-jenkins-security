pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/yahyaElmjiyed/tp-jenkins-security.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                docker run --rm -v $PWD:/app -w /app python:3.10 \
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                docker run --rm -v $PWD:/app -w /app python:3.10 \
                pytest
                '''
            }
        }

        stage('SCA Scan') {
            steps {
                echo "Security scan stage"
            }
        }

    }

    post {
        failure {
            echo 'Build failed due to errors or vulnerabilities'
        }
    }
}
