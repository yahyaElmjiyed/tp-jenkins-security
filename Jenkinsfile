pipeline {
    agent {
        docker {
            image 'python:3.10'
        }
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/yahyaElmjiyed/tp-jenkins-security.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('SCA Scan') {
            steps {
                echo "Dependency check stage"
            }
        }
    }

    post {
        failure {
            echo 'Build failed due to errors or vulnerabilities'
        }
    }
}
