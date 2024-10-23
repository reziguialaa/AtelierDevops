pipeline {
    agent any
    tools {
        maven 'M2_HOME' 
    }

    environment {
        NEXUS_URL = 'http://localhost:8081/repository/maven-releases/'
        NEXUS_CREDENTIALS = '582e4716-0415-4408-a261-5766d6d82697'  
        MAVEN_GROUP_ID = 'tn.esprit.spring.services'
        MAVEN_ARTIFACT_ID = 'timesheet-devops'
        MAVEN_VERSION = '1.0'
    }

    stages {
        stage('Checkout') {
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
                script {
                    sh """
                    mvn deploy:deploy-file \
                      -DgroupId=${MAVEN_GROUP_ID} \
                      -DartifactId=${MAVEN_ARTIFACT_ID} \
                      -Dversion=${MAVEN_VERSION} \
                      -Dpackaging=jar \
                      -DrepositoryId=deploymentRepo \
                      -Durl=${NEXUS_URL} \
                      -Dfile=target/${MAVEN_ARTIFACT_ID}-${MAVEN_VERSION}.jar
                    """
                }
            }
        }
    }
}
