pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
                git branch: 'feature/2026.06.17', url: 'https://github.com/Harishprathi/onlinebookstore.git'
            }
        }
stage('build') {
            steps {
                bat 'mvn install'
            }
        }

stage('test') {
            steps {
                bat 'mvn test'
            }
        }

stage('genaerate artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
        }


stage('deploy') {
            steps {
                
deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcatcredentials', path: '', url: 'http://localhost:8080/')], contextPath: null, war: 'target/*.war'   }
        }





    }
}
