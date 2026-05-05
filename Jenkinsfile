pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Riyaz-ryz007/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit Security Scan') {
            steps {
                sh 'npm audit || true'
            }
        }

        stage('SonarCloud Analysis') {
    steps {
        sh '''
        npm install sonar-scanner --save-dev

        npx sonar-scanner \
        -Dsonar.projectKey=Riyaz-ry2007_8.2CDevSecOps \
        -Dsonar.organization=Riyaz-ry2007 \
        -Dsonar.sources=. \
        -Dsonar.host.url=https://sonarcloud.io \
        -Dsonar.login=$SONAR_TOKEN
        '''
    }
}
    }
}
