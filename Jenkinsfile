pipeline {

    agent any

    stages {

        stage('Setup Python') {
            steps {
                sh '''
                cd app
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                cd app
                . venv/bin/activate
                python -m pytest -v
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                cd app
                sh docker build -t monitoring-app .
                '''

            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose up -d'
            }
        }
    }
}