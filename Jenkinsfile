pipeline {
    agent any

    environment {
        VENV = "venv"
        DEPLOY_DIR = "C:\\flask_deploy"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/aliza0902/flaskjenkinsapp.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                python -m venv %VENV%
                %VENV%\\Scripts\\activate
                python -m pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat '''
                %VENV%\\Scripts\\activate
                pytest
                '''
            }
        }

        stage('Build Application') {
            steps {
                bat '''
                mkdir build
                copy app.py build\\
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                bat '''
                mkdir %DEPLOY_DIR%
                xcopy build\\* %DEPLOY_DIR% /Y
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
