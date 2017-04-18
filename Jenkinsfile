pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }    

        stage('Build') {
            steps {
                withDockerContainer('java:8') {
                    sh './gradlew clean compile'
                }
            }
        }

        stage('Verify') {
            steps {
                withDockerContainer('java:8') {
                    sh './gradlew check'
                }        
            }            
        }
    }
}



