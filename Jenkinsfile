node {    
    stage('Checkout') {
        checkout scm
    }    

    stage('Build') {
        docker.image('openjdk:8').inside {
            sh './gradlew clean compile'
        }
    }

    stage('Verify') {
        docker.image('openjdk:8').inside {
            sh './gradlew check'
        }        
    }
}



