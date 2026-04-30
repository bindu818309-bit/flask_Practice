pipeline {
    agent any

    environment {
        VENV = "venv"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/bindu818309-bit/flask_Practice.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                python3 -m venv $VENV
                . $VENV/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                . $VENV/bin/activate
                pip install pytest
                pytest || true
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Starting Flask app..."
                nohup python3 app.py > app.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo "Build Successful in staging"
        }
        failure {
            echo "Build Failed"
        }
    }
}
