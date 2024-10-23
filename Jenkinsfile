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
                script {
                    def nexusUrl = 'http://192.168.152.130:8081/repository/maven-releases/'
                    def groupId = 'tn.esprit.spring.services'
                    def artifactId = 'timesheet-devops'
                    def version = '1.0'
                    def packaging = 'jar'

                    // Use the correct credentials ID
                    withCredentials([usernamePassword(credentialsId: '582e4716-0415-4408-a261-5766d6d82697', usernameVariable: 'NEXUS_USER', passwordVariable: 'NEXUS_PASSWORD')]) {
                        sh "mvn deploy:deploy-file -DgroupId=${groupId} " +
                           "-DartifactId=${artifactId} " +
                           "-Dversion=${version} " +
                           "-Dpackaging=${packaging} " +
                           "-Dfile=target/${artifactId}-${version}.${packaging} " +
                           "-DrepositoryId=maven-releases " +
                           "-Durl=${nexusUrl} " +
                           "-DskipTests=true " +
                           "-Dusername=${NEXUS_USER} " +
                           "-Dpassword=${NEXUS_PASSWORD}"
                    }
                }
            }
        }
    }
}
