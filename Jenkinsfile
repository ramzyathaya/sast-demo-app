pipeline {
    agent any
    environment {
        // Make sure pip installed path is accessible to Jenkins
        PATH = "/Users/ramzy/Library/Python/3.9/bin:${env.PATH}"
    }
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure pip3 is available and use it to install Bandit
                    sh 'python3 -m pip install --user bandit'
                }
            }
        }
        stage('SAST Analysis') {
            steps {
                script {
                    // Run Bandit for Static Analysis
                    sh 'bandit -f xml -o bandit-output.xml -r .'
                }
            }
        }
        stage('Archive Results') {
            steps {
                // Archiving the bandit output report for later review
                archiveArtifacts artifacts: 'bandit-output.xml', allowEmptyArchive: true
            }
        }
    }
    post {
        always {
            // Clean up any files after the build
            cleanWs()
        }
    }
}
