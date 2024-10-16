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
                    sh 'mvn sonar:sonar -D sonar.projectKey=AtelierDevops -D sonar.token=sqa_8317ed8683a0540f9245256fb7cf98304e4088ed'
                }
            }
        }
    }
}
