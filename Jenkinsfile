pipeline {
    agent any

    stages {

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

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=python-sonar-demo \
                          -Dsonar.sources=.
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                sh '''
                    mkdir -p dist
                    tar -czf dist/python-junit-demo-1.0.0.tar.gz app.py test_app.py
                '''
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts 'dist/*.tar.gz'
            }
        }
    }
}