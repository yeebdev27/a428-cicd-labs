node {
    stage('Check directory') {
        checkout scm
        sh  'git config --global --add safe.directory "*"'
        sh  'ls -l'
    }
    nodejs('node-latest') {
        stage('Build') {
            sh  'npm install'
        }
        stage('Test') {
            sh  './jenkins/scripts/test.sh'
        }
    }
}