pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'main',
                url: 'https://github.com/reziguialaa/AtelierDevops.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=AtelierDevops'
                }
            }
        }
    }
}
