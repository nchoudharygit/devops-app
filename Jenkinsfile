pipeline {
    // BUG 1: 'agent any' doesn't guarantee Python 3.11 is available.
    // Change to a Docker agent using python:3.11-slim.
    agent {
        docker {
            image 'python:3.11-slim'
        }
    }

    options {
        // BUG 4: 10 hours is way too long for a unit test suite — use 15 minutes
        timeout(time: 15, unit: 'MINUTES')
        disableConcurrentBuilds() // Prevent multiple builds from running simultaneously
    }

    stages {
        stage('Install') {
            steps {
                // BUG 2: Installing globally without a virtualenv
                // May conflict with system Python or other builds
             sh '''
                 python -m venv venv
                 . venv/bin/activate
                 pip install -r requirements.txt pytest
             '''
            }   
              
        }

        stage('Test') {
            steps {
                sh 'pytest --junitxml=test-results.xml'
            }
            post {
                always {
                    // BUG 3: This glob doesn't match — check the actual output path
                    junit '**/test-results.xml'
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            // BUG 5: No when condition — runs on ALL branches including feature branches
            steps {
                sh 'echo "Deploying to production..."'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed!'
        }
    }
}
