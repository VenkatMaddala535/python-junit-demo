pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                sh '''
                    python3 -m pip install pytest
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    mkdir -p reports
                    python3 -m pytest --junitxml=reports/junit.xml
                '''
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'reports/junit.xml'
            }
        }
    }
}