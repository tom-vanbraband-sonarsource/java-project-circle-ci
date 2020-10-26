pipeline {    
    agent any
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/tom-vanbraband-sonarsource/java-project-circle-ci.git'
            }
        }
        stage('Build') {
            tools {
                jdk "jdk-1.8.101"
            }
            steps {
                sh 'mvn compile'
            }
        }
        stage('SonarCloud analysis') {
            tools {
                jdk "openjdk-11"
            }
            environment {
                scannerHome = tool '4.2.0'
            }
            steps {
                withSonarQubeEnv(installationName: 'SonarCloud', credentialsId: 'customCredentialsId') {
                    sh "${scannerHome}/bin/sonar-scanner -X"
                } // submitted SonarQube taskId is automatically attached to the pipeline context
            }
        }
    }
}
