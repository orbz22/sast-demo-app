pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/orbz22/sast-demo-app.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Membuat virtual environment
                    sh 'python3 -m venv venv'
                    // Mengaktifkan virtual environment dan menginstal bandit
                    sh '. venv/bin/activate && pip install bandit'
                }
            }
        }
        stage('SAST Analysis') {
            steps {
                // Menjalankan analisis SAST dengan Bandit di dalam virtual environment
                sh '. venv/bin/activate && bandit -f xml -o bandit-output.xml -r . || true'
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
            }
        }
    }
}
