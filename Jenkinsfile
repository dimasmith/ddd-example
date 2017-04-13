stage 'Build'
node {
    checkout scm
    sh './gradlew clean classes'
}

stage 'Verify'
node {
    sh './gradlew check'
}

