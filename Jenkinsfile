pipeline {
    agent any

    tools {
        nodejs 'nodejs-18.16.1'
    }

    environment {
        SONARQUBE_TOKEN = credentials('mernbackend')
        SONAR_SCANNER_PATH = 'C:/Users/Monisha/Downloads/sonar-scanner-6.2.1.4610-windows-x64/bin'
        NODEJS_HOME = 'C:/Program Files/nodejs'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                set PATH=%NODEJS_HOME%;%PATH%
                npm install --verbose
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                
                    bat '''
                        set PATH=%SONAR_SCANNER_PATH%;%PATH%
                        where sonar-scanner || echo "SonarQube scanner not found. Please install it."
                        sonar-scanner.bat -D"sonar.projectKey=mernbackend" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.token=sqp_9a99359d2b457de7a9a9c9193b642b6203a7de0c"
                    '''
                
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
