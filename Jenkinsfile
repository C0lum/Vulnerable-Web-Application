pipeline {
    agent any

    stages {
        stage ('Checkout') {
            steps {
                git branch:'master', url: 'https://github.com/C0lum/Vulnerable-Web-Application.git'
            }
        }

        stage ('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube Scanner';
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
    
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube() 
        }
    }
}