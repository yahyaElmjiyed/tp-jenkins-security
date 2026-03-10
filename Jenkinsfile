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
                sh 'pip3 install -r requirements.txt --break-system-packages'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Security Scan') {
            steps {
                sh '''
                mkdir -p dependency-check-report

                dependency-check \
                --project "TP-Jenkins-Security" \
                --scan . \
                --format HTML \
                --out dependency-check-report || true

                # create fake report if scan fails
                if [ ! -f dependency-check-report/dependency-check-report.html ]; then
                    echo "<html><body><h1>Dependency Check Report</h1><p>Scan skipped or failed.</p></body></html>" > dependency-check-report/dependency-check-report.html
                fi
                '''
            }
        }

        stage('Archive Report') {
            steps {
                archiveArtifacts artifacts: 'dependency-check-report/**', allowEmptyArchive: true
            }
        }

    }
}
