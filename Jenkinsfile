
pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading project from GitHub...'

                git branch: 'main',
                url: 'https://github.com/YOUR_USERNAME/Jenkins-CICD-Project.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the web project...'

                bat 'dir'

                bat 'if exist index.html (echo HTML file found) else (exit /b 1)'
                bat 'if exist style.css (echo CSS file found) else (exit /b 1)'
                bat 'if exist script.js (echo JS file found) else (exit /b 1)'
            }
        }

        stage('Test') {
            steps {
                echo 'Validating HTML using HTML Tidy...'

                bat 'tidy -q -e index.html'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website to IIS...'

                bat 'if not exist "%DEPLOY_DIR%" exit /b 1'

                bat 'copy /Y index.html "%DEPLOY_DIR%\\index.html"'
                bat 'copy /Y style.css "%DEPLOY_DIR%\\style.css"'
                bat 'copy /Y script.js "%DEPLOY_DIR%\\script.js"'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
            echo 'Visit http://localhost/'
        }

        failure {
            echo 'Pipeline failed! Check console output.'
        }
    }
}
