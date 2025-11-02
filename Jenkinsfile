pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'python3 main.py'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m pytest'
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
                // build duration
                def status = currentBuild.currentResult
                def duration = currentBuild.duration / 1000.0

                // MySQL
                sh "python3 /scripts/log_to_db.py --project ${JOB_NAME} --status ${status} --build-number $BUILD_NUMBER --duration ${duration}"
            }
        }
    }
}
