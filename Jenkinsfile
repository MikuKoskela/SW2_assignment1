pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
        jdk 'JAVA_17'
        git 'GIT-HOME'
    }

    environment {
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('mvn clean and compile') {
            steps {
                bat 'mvn clean compile'            }
        }

        stage('mvn test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('mvn deploy') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'mvn jacoco:report'
            }
        }

    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        success {
            echo 'Build succeeded'
        }
        failure {
            echo 'Build failed'
        }
    }
}