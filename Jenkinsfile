node {    
    stage('Checkout') {
        checkout scm
    }    

    stage('Build') {
        docker.image('openjdk:8').inside {
            sh './gradlew clean compileJava'
        }
    }

    stage('Verify') {
        docker.image('openjdk:8').inside {
            sh './gradlew check'
        }        
    }
}



