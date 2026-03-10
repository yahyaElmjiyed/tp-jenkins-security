pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/yahyaElmjiyed/tp-jenkins-security.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                sh 'pip3 install -r requirements.txt --break-system-packages'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running pytest tests...'
                sh 'pytest'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running OWASP Dependency Check...'
                sh '''
                mkdir -p dependency-check-report
                mkdir -p dependency-check-data

                dependency-check \
                --project "TP-Jenkins-Security" \
                --scan . \
                --format HTML \
                --out dependency-check-report \
                --data dependency-check-data \
                --noupdate
                '''
            }
        }

        stage('Archive Report') {
            steps {
                archiveArtifacts artifacts: 'dependency-check-report/**', fingerprint: true
            }
        }

    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
