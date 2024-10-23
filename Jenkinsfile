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
                def nexusUrl = 'http://localhost:8081/repository/maven-releases/'
                def groupId = 'tn.esprit.spring.services'
                def artifactId = 'timesheet-devops'
                def version = '1.0'
                def packaging = 'jar'

                // Deploy the artifact to Nexus
                sh "mvn deploy:deploy-file -DgroupId=${groupId} " +
                   "-DartifactId=${artifactId} " +
                   "-Dversion=${version} " +
                   "-Dpackaging=${packaging} " +
                   "-Dfile=target/${artifactId}-${version}.${packaging} " +
                   "-DrepositoryId=deploymentRepo " +
                   "-Durl=${nexusUrl} " +
                   "-DskipTests=true"
            }
        }
    }
}
