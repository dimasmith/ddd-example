node {
    stage('Checkout') {
        checkout scm
    }    

    stage('Build') {
        withDockerContainer('java:8') {
            sh './gradlew clean compile'
        }
    }

    stage('Verify') {
        withDockerContainer('java:8') {
            sh './gradlew check'
        }        
    }
}
