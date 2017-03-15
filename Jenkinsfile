stage('Build') {
    node {
        git url: 'https://github.com/dimasmith/ddd-example.git', branch: 'dev'
        sh './gradlew clean test'
    }
}

