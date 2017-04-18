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
                withDockerContainer('openjdk:8') {
                    sh './gradlew clean compile'
                }
            }
        }

        stage('Verify') {
            steps {
                withDockerContainer('openjdk:8') {
                    sh './gradlew check'
                }        
            }            
        }
    }
}



