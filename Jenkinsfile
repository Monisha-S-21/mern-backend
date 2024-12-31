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
            sh 'node -v'      // Verify Node.js version
            sh 'npm -v'       // Verify npm version
            sh 'npm cache clean --force'
            sh 'npm install --verbose'  // Verbose output
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
            echo 'Backend pipeline completed successfully.'
        }
        failure {
            echo 'Backend pipeline failed.'
        }
    }
}
