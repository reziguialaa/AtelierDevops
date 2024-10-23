pipeline {
    agent any
    
    tools {
        maven 'M2_HOME' // Adjust this if your Maven tool is configured differently
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
                withMaven(settings: 'path/to/your/settings.xml') { 
                    sh 'mvn deploy'
                }
            }
        }
    }
}
