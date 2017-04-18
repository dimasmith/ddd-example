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
                docker.image('openjdk:8').inside {
                    sh './gradlew clean compile'
                }
            }
        }

        stage('Verify') {
            steps {
                docker.image('openjdk:8').inside {
                    sh './gradlew check'
                }        
            }            
        }
    }
}



