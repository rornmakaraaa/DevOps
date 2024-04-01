pipeline {
    agent any // window agent, Jenkins-laravel (other machine)

    stages {
        stage('Fetch from GitHub') { //build steps
            steps {
                echo 'Fetching for GitHub'
                git branch: 'tp3' , url: 'https://github.com/rornmakaraaa/DevOps.git'
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
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"926264458\", \"text\": \"[SUCCESS] This project is build success!\", \"disable_notification\": false}\' https://api.telegram.org/bot6993552728:AAFrkhDAN3UiIUnDIvkDazVJpkZMLPnMTF8/sendMessage'
        }
        failure {
            sh 'curl -X POST -H "Content-Type: application/json" -d \'{\"chat_id\": \"926264458\", \"text\": \"[FAILED] This project is build failed!\", \"disable_notification\": false}\' https://api.telegram.org/bot6993552728:AAFrkhDAN3UiIUnDIvkDazVJpkZMLPnMTF8/sendMessage'
        }
    }
}