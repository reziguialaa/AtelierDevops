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
        stage('Deploy to Nexus') {
            steps {
                    sh 'mvn deploy -s ~/.m2/settings.xml -X'
            }
        }
      
    }
}
