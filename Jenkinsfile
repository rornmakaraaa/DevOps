pipeline {
    agent any // window agent, Jenkins-laravel (other machine)

    stages {
        stage('Fetch from GitHub') { //build steps
            steps {
                echo 'Fetching for GitHub'
                git branch: 'TP03' , url: 'https://github.com/POMMOUYLANG/DevOps-TP-Jenkins-.git'
            }
        }
        stage('Composer install') { 
            steps {
                sh 'composer install'
            }
        }
        stage('Copy .env') { 
            steps {
                sh 'cp .env.example .env'
            }
        }
        stage('Add key') { 
            steps {
                echo 'running code ...'
                sh 'php artisan key:generate'
            }
        }
        stage('npm') { 
            steps {
                echo 'Compiling code ...'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test the app'){
            steps{
                echo 'Testing unit tests...'
                echo 'Testing feature...'
                sh 'php artisan test'
            }
        }
    }
    // Telegram Notification
    post {
        success {
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"1003515001\", \"text\": \"[SUCCESS] Ukata api build success!\", \"disable_notification\": false}\' https://api.telegram.org/bot6654457291:AAF8XhNC9HPwMIhgk4DTIcYvpe2o0qoX70o/sendMessage'
        }
        failure {
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"1003515001\", \"text\": \"[FAILED] Ukata api build failed!\", \"disable_notification\": false}\' https://api.telegram.org/bot6654457291:AAF8XhNC9HPwMIhgk4DTIcYvpe2o0qoX70o/sendMessage'
        }
    }
}