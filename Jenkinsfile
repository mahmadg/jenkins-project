pipeline {
    agent any
    environment {
        APP_NAME = "my-webapp"
    }
    tools {
        maven 'maven-3.9.6'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'dmz_web', url: 'https://github.com/mahmadg/jenkins-project.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [
                    tomcat9(
            credentialsId: 'ad616399-3268-4ec7-84e7-4cd4e00b6e29', 
                        path: '', 
                        url: 'http://192.168.1.201:8080')
        ], contextPath: 'my-webapp', war: 'target/my-webapp.war'}
        }
    }
    post {
        success {
            echo "Deployed! Access: http://192.168.1.201:8080/${my-webapp}"
        }
    }
}





