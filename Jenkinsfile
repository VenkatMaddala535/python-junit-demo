pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                sh 'pytest --junitxml=reports/junit.xml'
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'reports/junit.xml'
            }
        }
    }
}