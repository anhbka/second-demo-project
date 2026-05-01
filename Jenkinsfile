pipeline {
    agent any

    tools {
        maven 'maven-3.9.14'
        jdk 'java-17'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', 
                    url: 'https://github.com/anhbka/second-demo-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', 
                          allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true, 
                  testResults: 'target/surefire-reports/*.xml'
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}