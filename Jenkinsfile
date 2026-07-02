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
        
         stage('sonarcube analysis') {
            steps {
               bat '''mvn install sonar:sonar \
  -Dsonar.projectKey=Onlinebookstore \
  -Dsonar.projectName='Onlinebookstore' \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=sqp_19ca17ea97ce78295deecea02b126857f84499b7'''
            }
        }
         stage('Generate artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
        }
        
        
   stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcatcredentials', path: '', url: 'http://localhost:8080/')], contextPath: 'My online book store', war: 'target/*.war'
            }
        }     
        
    }
}
