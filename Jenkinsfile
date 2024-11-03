pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube_server') {
                       
                        sh 'sonar-scanner -Dsonar.projectKey=myProjectKey -Dsonar.sources=src -Dsonar.login=$SONARQUBE_TOKEN'
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'SonarQube analysis completed successfully!'
        }
        failure {
            echo 'SonarQube analysis failed!'
        }
    }
}
