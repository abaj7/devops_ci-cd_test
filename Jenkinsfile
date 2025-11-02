pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'python3 main.py'
                // Add your build commands here
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add test commands like 'pytest' if needed
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh 'python3 /scripts/deploy.py'
            }
        }
    }

    post {
        always {
            script {
                // Jenkins build info
                def status = currentBuild.currentResult
                def duration = currentBuild.duration / 1000.0 // in seconds

                // Log to MySQL
                sh "python3 /scripts/log_to_db.py --project MyProject --status ${status} --build-number $BUILD_NUMBER --duration ${duration}"
            }
        }
    }
}
