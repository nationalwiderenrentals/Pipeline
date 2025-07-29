pipeline {
    agent any

    tools {
        maven 'Maven 3.8.5'  // Make sure it's configured in Jenkins
        jdk 'JDK 11'         // Also configure this in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/nationalwiderenrentals/Pipeline.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
