stage 'Build'
node {
    git url: 'https://github.com/dimasmith/ddd-example.git', branch: 'dev'
    sh './gradlew clean classes'
}

stage 'Verify'
node {
    sh './gradlew check'
}

stage 'Deploy'
timeout(time:1, unit:'HOURS') {
    input message:'Approve deployment?'
}
node {
    sh './gradlew uploadArchives'
}
