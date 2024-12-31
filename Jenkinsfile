pipeline {
    agent any

    tools {
        nodejs 'nodejs-18.16.1'
    }

    environment {
        SONARQUBE_TOKEN = credentials('mernbackend')
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube Scanner') { // Ensure this matches your SonarQube configuration
                        sh '''
                            npm run sonar -- \
                            -Dsonar.projectKey=mernbackend \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.token=$SONAR_TOKEN
                        '''
                    }
            }
        }
    }
  post {
        success {
            echo 'Frontend pipeline completed successfully.'
        }
        failure {
            echo 'Frontend pipeline failed.'
        }
    }
}
