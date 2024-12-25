pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    
                    def selectedBranch = env.BRANCH_NAME ?: 'master'
                    git branch: selectedBranch, url: 'https://github.com/FaridBayu/ppmpl_2200016048_muhammad-farid-bayu-hadi_prak8.git'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Unit Tests') {
            when {
                branch 'master'
            }
            steps {
                bat 'npm test'
            }
        }
        stage('Run Integration Tests') {
            when {
                branch 'master'
            }
            steps {
                bat 'npm run test:integration'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Tambahkan perintah build jika diperlukan
            }
        }
        stage('Deploy to Staging') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to staging server...'
                sh 'scp -r ./build user@staging-server:/var/www/app'
                sh 'ssh user@staging-server "systemctl restart app-service"'
            }
        }
    }
    post {
        success {
            echo 'Pipeline finished successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
