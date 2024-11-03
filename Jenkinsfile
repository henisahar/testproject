pipeline {
    agent any

    environment {
        SONARQUBE_ENV = 'SonarQube_server'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/develop']],
                    userRemoteConfigs: [[url: 'https://github.com/henisahar/testproject.git']]
                ])
            }
        }

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm config get registry'
                bat 'npm config set registry https://registry.npmjs.org/'
                bat 'npm install -g yarn'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv(SONARQUBE_ENV) {
                        bat "npx sonar-scanner -Dsonar.projectKey=trello-app -Dsonar.projectName=trello-app -Dsonar.projectVersion=1.0 -Dsonar.sources=. -Dsonar.sourceEncoding=UTF-8 -Dsonar.token=${sonarqube-token} -Dsonar.exclusions=**/node_modules/**"
                    }
                }
            }
        }
    }
}
