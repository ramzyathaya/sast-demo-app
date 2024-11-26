pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Clone the repository from GitHub
                git url: 'https://github.com/ramzyathaya/sast-demo-app.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install Bandit, a Python static code analysis tool
                sh 'pip3 install bandit'
            }
        }
        stage('SAST Analysis') {
            steps {
                // Run Bandit and save the output in XML format
                sh 'bandit -f xml -o bandit-output.xml -r . || true'
                
                // Record SAST issues using Jenkins' Warnings Next Generation Plugin
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
            }
        }
    }
}
