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
                sh 'python3 -m pip install --user -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python3 -m pytest'
            }
        }

        stage('SCA Scan') {
            steps {
                echo "Dependency Check would run here"
            }
        }

    }

    post {
        failure {
            echo 'Build failed due to errors or vulnerabilities'
        }
    }
}
