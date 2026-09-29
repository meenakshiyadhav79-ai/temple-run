pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Validate static site files') {
            steps {
                echo 'Validating required project files...'
                sh '''
                    ls -la
                    test -f index.html
                    echo "index.html found"
                '''
            }
        }

        stage('Archive build output') {
            steps {
                echo 'Archiving project files...'
                archiveArtifacts artifacts: 'index.html, LICENSE', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build succeeded.'
        }
        failure {
            echo 'Build failed. Please check the logs.'
        }
    }
}
